---
title: "Spring Boot Database Replica Configuration - Primary-Replica 구성과 Read-Write Transaction Routing"
excerpt: "Spring Boot에서 H2 Database를 사용하여 Primary-Replica 이중화 구성을 구현하고, AOP 기반의 Read-Write Transaction Routing으로 자동 데이터소스 라우팅을 실현하는 방법"
last_modified_at: 2026-04-09T20:18:00
header:
  image: /assets/images/spring/database-replica-configuration.png
categories:
  - Spring
tags:
  - Programming
  - Spring Boot
  - Database
  - Replica
  - Transaction Routing
  - H2
  - AOP

toc: true
toc_ads: true
toc_sticky: true
---

# 개요

데이터베이스 부하 분산과 고가용성은 대규모 시스템에서 필수적인 요구사항입니다. 이 글에서는 **Spring Boot 애플리케이션에서 Primary-Replica(또는 Master-Slave) 데이터베이스 구성을 구현**하고, **AOP 기반의 자동 라우팅 메커니즘**을 통해 읽기(Read) 작업과 쓰기(Write) 작업을 효율적으로 분리하는 방법을 자세히 설명합니다.

이 예제에서는 **H2 메모리 데이터베이스** 2개를 Primary와 Replica로 구성하여 실제 운영 환경의 복제 구성을 시뮬레이션합니다.

---

# 1. 데이터베이스 Replica 구성의 개념

## 1.1 Primary-Replica란?

**Primary-Replica(또는 Master-Slave, Primary-Secondary) 구성**은 데이터베이스의 고가용성과 성능을 향상시키기 위한 아키텍처입니다.

### 구조
```
┌────────────────────────────────────┐
│     Application (Spring Boot)      │
│                                    │
│  ┌─────────────────────────────┐   │
│  │   DataSource Routing        │   │
│  │  (AbstractRoutingDataSource)│   │
│  └──────┬──────────────┬───────┘   │
│         │              │           │
│    (Write)        (Read)           │
│         │              │           │
│  ┌──────▼────┐   ┌─────▼──────┐    │
│  │  Primary  │   │  Replica   │    │
│  │(Read/Write)   │(Read-Only) │    │
│  └───────────┘   └────────────┘    │
│                                    │
│ 데이터 동기화 (Replication) ←─────┘  │
└────────────────────────────────────┘
```

### 특징

| 구성 | 특징 |
|------|------|
| **Primary** | 모든 쓰기 작업(INSERT, UPDATE, DELETE) 수행, 읽기도 가능 |
| **Replica** | Primary의 데이터를 동기화받음, 읽기(SELECT) 전용 |
| **동기화** | Primary의 변경사항이 Replica에 자동으로 전파됨 |

## 1.2 Primary-Replica 구성의 이점

1. **읽기 성능 향상**: 읽기 작업을 여러 Replica로 분산
2. **부하 분산**: 쓰기(Primary)와 읽기(Replica) 부하 분리
3. **고가용성**: Primary 장애 시 Replica로 페일오버 가능
4. **백업 용이**: Replica를 백업 용도로 사용 가능
5. **분석 작업**: 읽기 전용 Replica에서 무거운 분석 쿼리 수행

## 1.3 데이터베이스 선택: H2 vs 실제 DB

| DB | 개발 환경 | 테스트 | 운영 환경 |
|----|---------|--------|----------|
| **H2 (메모리)** | ✅ 완벽 | ✅ 완벽 | ❌ 권장 안함 |
| **MySQL** | ⭐ 가능 | ✅ 가능 | ✅ 권장 |
| **PostgreSQL** | ⭐ 가능 | ✅ 가능 | ✅ 권장 |
| **Oracle** | ⭐ 가능 | ✅ 가능 | ✅ 권장 |

> 이 글에서는 **H2 메모리 DB**를 사용하여 개발/테스트 환경에 최적화된 예제를 제공합니다.

---

# 2. 메커니즘: DataSource 라우팅 동작 방식

## 2.1 전체 요청 흐름

```
HTTP 요청
    ↓
Spring Controller
    ↓
Service 메서드 호출
    ↓
┌─────────────────────────────────────┐
│  AOP Aspect Interception            │
│                                     │
│  1. @ReadOnlyOnReplica 확인          │
│  2. @Transactional(readOnly) 확인    │
│  3. RouteDataSourceContext 업데이트  │
└────────────┬────────────────────────┘
             ↓
┌─────────────────────────────────┐
│ ReadWriteRoutingDataSource      │
│ determineCurrentLookupKey()     │
│ → RouteDataSourceContext 값 조회 │
│ → PRIMARY 또는 REPLICA 결정      │
└────────────┬────────────────────┘
             ↓
┌─────────────┬────────────────┐
│  PRIMARY DB │   REPLICA DB   │
│ (Write)     │   (Read)       │
└─────────────┴────────────────┘
```

## 2.2 핵심 클래스들의 상호작용

### RouteDataSourceContext (ThreadLocal 관리)
```java
public class RouteDataSourceContext {
    private static final ThreadLocal<DataSourceType> contextHolder 
        = ThreadLocal.withInitial(() -> DataSourceType.PRIMARY);
    
    // 각 스레드별로 독립적인 DataSource 타입 관리
}
```

**역할**: 각 스레드가 독립적으로 사용할 DataSource 타입을 관리합니다.

### ReadWriteRoutingDataSource (AbstractRoutingDataSource)
```java
public class ReadWriteRoutingDataSource extends AbstractRoutingDataSource {
    @Override
    protected Object determineCurrentLookupKey() {
        return RouteDataSourceContext.getDataSourceType();
    }
}
```

**역할**: Spring이 DB 접근 시점에 어떤 DataSource를 사용할지 결정합니다.

### DataSourceRoutingAspect (AOP Advice)
```java
@Aspect
public class DataSourceRoutingAspect {
    @Before("@annotation(com.gracefulsoul.replica.routing.ReadOnlyOnReplica)")
    public void beforeReadOnlyOnReplica(JoinPoint joinPoint) {
        RouteDataSourceContext.setReplica();
    }
    
    @After("@annotation(com.gracefulsoul.replica.routing.ReadOnlyOnReplica)")
    public void afterReadOnlyOnReplica(JoinPoint joinPoint) {
        RouteDataSourceContext.setPrimary();
    }
}
```

**역할**: 메서드 호출 전후에 DataSource 컨텍스트를 자동으로 변경합니다.

## 2.3 라우팅 규칙

```yaml
규칙 1: @ReadOnlyOnReplica 어노테이션
  ├─ public List<User> getAllUsers()          → REPLICA 사용
  └─ 메서드 종료 후 PRIMARY로 복원

규칙 2: @Transactional(readOnly = true)
  ├─ public Optional<User> getUserById(Long) → REPLICA 사용
  └─ 메서드 종료 후 PRIMARY로 복원

규칙 3: 일반 @Transactional (readOnly 없음)
  ├─ public User createUser(User)            → PRIMARY 사용
  └─ 메서드 종료 후 유지

규칙 4: 트랜잭션 없음 (기본값)
  └─ PRIMARY 사용 (기본값)
```

## 2.4 ThreadLocal을 사용한 멀티스레드 안전성

```java
// 스레드 A
thread_A.start_request()
  → RouteDataSourceContext.setReplica()  // Thread A의 컨텍스트만 변경
  → SELECT 수행
  → RouteDataSourceContext.setPrimary()

// 스레드 B (동시에 실행)
thread_B.start_request()
  → RouteDataSourceContext.setPrimary()  // Thread B의 컨텍스트만 변경
  → INSERT 수행
  → RouteDataSourceContext.setPrimary()

// 스레드 A와 B는 서로 영향을 주지 않음 ✓
```

**ThreadLocal의 장점**:
- 각 스레드별로 독립적인 저장소 제공
- 컨텍스트 전달 없이도 스레드 내 어디서나 접근 가능
- 멀티스레드 환경에서 동기화 문제 자동 해결

---

# 3. 내부 구조 상세 분석

## 3.1 프로젝트 디렉토리 구조

```
spring-boot-h2-replica/
├── src/main/java/com/gracefulsoul/replica/
│   ├── SpringBootH2ReplicaApplication.java
│   ├── aspect/
│   │   └── DataSourceRoutingAspect.java
│   ├── config/
│   │   └── DataSourceConfig.java
│   ├── controller/
│   │   └── UserController.java
│   ├── entity/
│   │   ├── User.java
│   │   └── UserLog.java
│   ├── repository/
│   │   ├── UserRepository.java
│   │   └── UserLogRepository.java
│   ├── routing/
│   │   ├── RouteDataSourceContext.java
│   │   ├── ReadWriteRoutingDataSource.java
│   │   └── ReadOnlyOnReplica.java
│   └── service/
│       ├── UserService.java
│       └── UserLogService.java
├── src/main/resources/
│   └── application.yml
├── src/test/java/com/gracefulsoul/replica/
│   ├── DataSourceContextTest.java
│   └── integration/
│       └── DataSourceRoutingIntegrationTest.java
└── pom.xml
```

## 3.2 설정 파일 상세분석

### application.yml
```yaml
spring:
  datasource:
    primary:
      url: jdbc:h2:mem:primary        # Primary용 H2 메모리 DB
      username: sa
      hikari:
        maximum-pool-size: 10
    
    replica:
      url: jdbc:h2:mem:replica        # Replica용 H2 메모리 DB
      username: sa
      hikari:
        maximum-pool-size: 10
```

**특징**:
- 별도의 메모리 DB 2개로 Primary/Replica 분리
- HikariCP로 연결 풀 관리
- 각각 독립적인 설정 가능

## 3.3 Entity 설계

### User Entity
```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String name;
    
    @Column(nullable = false, unique = true)
    private String email;
    
    @CreationTimestamp
    private LocalDateTime createdAt;
    
    @UpdateTimestamp
    private LocalDateTime updatedAt;
    
    @Version  // 낙관적 잠금
    private Long version;
}
```

**특징**:
- `@Version`: 동시성 제어 (낙관적 잠금)
- `@CreationTimestamp`: 자동으로 생성 시간 기록
- `@UpdateTimestamp`: 자동으로 수정 시간 기록

### UserLog Entity
```java
@Entity
@Table(name = "user_logs")
public class UserLog {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private Long userId;
    
    @Column(nullable = false)
    private String action;
    
    @CreationTimestamp
    private LocalDateTime createdAt;
}
```

**특징**:
- 로그 데이터이므로 UPDATE/DELETE 불필요
- PRIMARY KEY와 userId는 인덱싱 추천

## 3.4 Repository 디자인

### 쿼리별 DataSource 사용

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    // READ: Replica DataSource 사용
    Optional<User> findByEmail(String email);
    
    @Query("SELECT u FROM User u WHERE u.active = true")
    List<User> findAllActiveUsers();
    
    // WRITE: Primary DataSource 사용
    // save(), delete() 등 불필요 - 기본 제공
}
```

## 3.5 Service 계층의 라우팅 로직

```java
@Service
public class UserService {
    
    // 쓰기 작업: @Transactional (기본값)
    @Transactional  // readOnly 미지정 = PRIMARY 사용
    public User createUser(User user) {
        return userRepository.save(user);  // INSERT
    }
    
    // 읽기 작업: @Transactional(readOnly = true)
    @Transactional(readOnly = true)  // readOnly = true = REPLICA 사용
    public Optional<User> getUserById(Long id) {
        return userRepository.findById(id);  // SELECT
    }
    
    // 읽기 작업: @ReadOnlyOnReplica (대안)
    @ReadOnlyOnReplica
    public List<User> getAllUsers() {
        return userRepository.findAll();  // SELECT
    }
}
```

---

# 4. 주요 제품 및 기술 스택

## 4.1 사용된 기술

| 기술 | 버전 | 용도 |
|------|------|------|
| **Java** | 25 | 최신 언어 기능 활용 |
| **Spring Boot** | 3.3.0 | 애플리케이션 프레임워크 |
| **Spring Data JPA** | Latest | ORM 및 데이터 접근 |
| **Spring AOP** | Latest | 라우팅 메커니즘 구현 |
| **H2 Database** | 2.2.224 | 메모리 DB (개발/테스트) |
| **HikariCP** | 5.1.0 | 연결 풀 관리 |
| **Lombok** | Latest | 보일러플레이트 코드 제거 |
| **JUnit 5** | Latest | 단위 테스트 |

## 4.2 실제 운영 환경 권장 구성

### MySQL + Replication
```sql
-- Primary Server
CREATE USER 'replication'@'replica-server' IDENTIFIED BY 'password';
GRANT REPLICATION SLAVE ON *.* TO 'replication'@'replica-server';

-- Replica Server
CHANGE REPLICATION SOURCE TO
  SOURCE_HOST = 'primary-server',
  SOURCE_USER = 'replication',
  SOURCE_PASSWORD = 'password',
  SOURCE_LOG_FILE = 'mysql-bin.000001',
  SOURCE_LOG_POS = 154;

START REPLICA;
```

### PostgreSQL + Replication
```sql
-- Primary 설정 (postgresql.conf)
wal_level = replica
max_wal_senders = 3
max_replication_slots = 3

-- Replica 설정
pg_basebackup -h primary-server -D /var/lib/postgresql/data
```

---

# 5. 활용 샘플 및 코드

## 5.1 기본 CRUD 예제

### 사용자 생성 (Write - Primary 사용)
```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody User user) {
    return ResponseEntity.ok(userService.createUser(user));
}
```

**HTTP Request**:
```bash
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "name": "김준호",
    "email": "jhkim@example.com",
    "phone": "010-1234-5678",
    "active": true
  }'
```

**로그 출력**:
```
DataSourceRoutingAspect: 메서드 시작: UserService.createUser → PRIMARY DataSource 선택됨
```

### 사용자 조회 (Read - Replica 사용)
```java
@GetMapping("/users/{id}")
public ResponseEntity<User> getUserById(@PathVariable Long id) {
    return userService.getUserById(id)
        .map(ResponseEntity::ok)
        .orElse(ResponseEntity.notFound().build());
}
```

**HTTP Request**:
```bash
curl -X GET http://localhost:8080/api/users/1
```

**로그 출력**:
```
DataSourceRoutingAspect: 메서드 시작: UserService.getUserById → REPLICA DataSource 선택됨
```

## 5.2 복잡한 쿼리 예제

### 검색 및 필터링
```java
@Service
public class UserService {
    
    @ReadOnlyOnReplica("사용자명으로 검색")
    public List<User> searchUsers(String name) {
        return userRepository.searchByName(name);
    }
    
    @Transactional(readOnly = true)
    public List<User> getActiveUsers() {
        return userRepository.findAllActiveUsers();
    }
    
    @ReadOnlyOnReplica("활성 사용자 수 카운트")
    public long countActiveUsers() {
        return userRepository.countByActive(true);
    }
}
```

### 복합 트랜잭션
```java
@Service
@RequiredArgsConstructor
public class TransactionService {
    private final UserRepository userRepository;
    private final UserLogRepository userLogRepository;
    
    // 1단계: 사용자 수정 (Primary)
    // 2단계: 로그 기록 (Primary)
    @Transactional
    public void updateUserWithLog(Long userId, User updateData) {
        User user = userRepository.findById(userId)
            .orElseThrow(() -> new IllegalArgumentException("사용자 없음"));
        
        user.setName(updateData.getName());
        userRepository.save(user);
        
        UserLog log = UserLog.builder()
            .userId(userId)
            .action("UPDATE")
            .description("사용자 정보 수정")
            .ipAddress("192.168.1.1")
            .build();
        userLogRepository.save(log);
    }
    
    // 1단계: 사용자 조회 (Replica)
    // 2단계: 로그 조회 (Replica)
    @Transactional(readOnly = true)
    public UserProfile getUserProfile(Long userId) {
        User user = userRepository.findById(userId)
            .orElseThrow(() -> new IllegalArgumentException("사용자 없음"));
        
        List<UserLog> logs = userLogRepository.findByUserId(userId);
        
        return UserProfile.builder()
            .user(user)
            .logs(logs)
            .build();
    }
}
```

## 5.3 배치 작업 예제

```java
@Service
@RequiredArgsConstructor
public class UserBatchService {
    private final UserRepository userRepository;
    
    // 배치 INSERT: Primary 사용
    @Transactional
    public void batchCreateUsers(List<User> users) {
        users.forEach(userRepository::save);
    }
    
    // 배치 SELECT: Replica 사용
    @ReadOnlyOnReplica("전체 사용자 배치 조회")
    public List<User> batchGetAllUsers(int batchSize) {
        return userRepository.findAll();
    }
    
    // 일괄 업데이트: Primary 사용
    @Transactional
    public void batchUpdateUsersStatus(List<Long> userIds, Boolean active) {
        userRepository.findAllById(userIds)
            .forEach(user -> user.setActive(active));
    }
}
```

---

# 6. 주요 코드 설명

## 6.1 RouteDataSourceContext 상세분석

```java
public class RouteDataSourceContext {
    // ThreadLocal: 각 스레드별 독립적인 저장소
    private static final ThreadLocal<DataSourceType> contextHolder 
        = ThreadLocal.withInitial(() -> DataSourceType.PRIMARY);
    
    // DataSource 설정
    public static void setDataSourceType(DataSourceType dataSourceType) {
        contextHolder.set(dataSourceType);  // 스레드 안전
    }
    
    // DataSource 조회
    public static DataSourceType getDataSourceType() {
        return contextHolder.get();
    }
    
    // 초기화
    public static void clear() {
        contextHolder.set(DataSourceType.PRIMARY);
    }
}
```

**핵심 개념**:
- `ThreadLocal.withInitial()`: 초기값 설정
- `set()`: 현재 스레드의 값 설정
- `get()`: 현재 스레드의 값 조회
- 스레드마다 독립적인 저장소로 동기화 문제 해결

## 6.2 ReadWriteRoutingDataSource 상세분석

```java
public class ReadWriteRoutingDataSource extends AbstractRoutingDataSource {
    
    // 핵심: Spring이 DB 접근 직전 이 메서드 호출
    @Override
    protected Object determineCurrentLookupKey() {
        // 1. 현재 컨텍스트에서 DataSource 타입 조회
        DataSourceType type = RouteDataSourceContext.getDataSourceType();
        
        // 2. 해당 타입의 DataSource 반환
        // 이 객체는 targetDataSources Map에 저장된 DataSource를 찾음
        return type;
    }
}
```

**호출 순서**:
```
1. Service 메서드 호출
   ↓
2. AOP Aspect가 메서드 가로채기
   ↓
3. RouteDataSourceContext 업데이트
   ↓
4. Repository 메서드 호출 (JPA)
   ↓
5. AbstractRoutingDataSource.determineCurrentLookupKey() 호출
   ↓
6. 적절한 DataSource 반환
   ↓
7. DB 작업 수행
```

## 6.3 DataSourceConfig 상세분석

```java
@Configuration
public class DataSourceConfig {
    
    // Primary DataSource Bean (Write용)
    @Bean(name = "primaryDataSource")
    @ConfigurationProperties(prefix = "spring.datasource.primary")
    public DataSource primaryDataSource() {
        return DataSourceBuilder.create()
            .driverClassName("org.h2.Driver")
            .build();
    }
    
    // Replica DataSource Bean (Read용)
    @Bean(name = "replicaDataSource")
    @ConfigurationProperties(prefix = "spring.datasource.replica")
    public DataSource replicaDataSource() {
        return DataSourceBuilder.create()
            .driverClassName("org.h2.Driver")
            .build();
    }
    
    // 라우팅 DataSource (Primary Bean)
    @Bean
    @Primary
    public DataSource routingDataSource(
            @Autowired DataSource primaryDataSource,
            @Autowired(name = "replicaDataSource") DataSource replicaDataSource) {
        
        ReadWriteRoutingDataSource routingDataSource = new ReadWriteRoutingDataSource();
        
        // 라우팅 맵 설정
        Map<Object, Object> targetDataSources = new HashMap<>();
        targetDataSources.put(DataSourceType.PRIMARY, primaryDataSource);
        targetDataSources.put(DataSourceType.REPLICA, replicaDataSource);
        
        routingDataSource.setTargetDataSources(targetDataSources);
        routingDataSource.setDefaultTargetDataSource(primaryDataSource);
        
        return routingDataSource;
    }
}
```

**특징**:
- `@ConfigurationProperties`: YAML 설정과 자동 매핑
- `@Primary`: 여러 DataSource 중 기본값으로 사용
- `targetDataSources`: 라우팅할 DataSource 맵

## 6.4 DataSourceRoutingAspect 상세분석

```java
@Aspect
@Component
public class DataSourceRoutingAspect {
    
    // @ReadOnlyOnReplica 메서드 호출 전
    @Before("@annotation(com.gracefulsoul.replica.routing.ReadOnlyOnReplica)")
    public void beforeReadOnlyOnReplica(JoinPoint joinPoint, ReadOnlyOnReplica readOnlyOnReplica) {
        String methodName = joinPoint.getSignature().getName();
        String className = joinPoint.getTarget().getClass().getSimpleName();
        
        // Replica로 설정
        RouteDataSourceContext.setReplica();
        log.debug("메서드 시작: {}.{} -> Replica DataSource 선택됨", 
                 className, methodName);
    }
    
    // @ReadOnlyOnReplica 메서드 호출 후
    @After("@annotation(com.gracefulsoul.replica.routing.ReadOnlyOnReplica)")
    public void afterReadOnlyOnReplica(JoinPoint joinPoint) {
        // Primary로 복원
        RouteDataSourceContext.setPrimary();
    }
    
    // @Transactional(readOnly = true) 메서드 호출 전
    @Before("@annotation(org.springframework.transaction.annotation.Transactional)")
    public void beforeTransactionalMethod(JoinPoint joinPoint, Transactional transactional) {
        if (transactional.readOnly()) {
            RouteDataSourceContext.setReplica();
        }
    }
}
```

**AOP 포인트컷**:
- `@annotation()`: 특정 어노테이션 대상 메서드
- `@Before`: 메서드 실행 전 실행
- `@After`: 메서드 실행 후 실행

---

# 7. 테스트 전략

## 7.1 단위 테스트

```java
@SpringBootTest
class DataSourceContextTest {
    
    @Test
    @DisplayName("DataSourceContext 기본값이 PRIMARY")
    void testDefaultDataSourceContext() {
        RouteDataSourceContext.clear();
        assertThat(RouteDataSourceContext.getDataSourceType())
            .isEqualTo(DataSourceType.PRIMARY);
    }
    
    @Test
    @DisplayName("setReplica()로 REPLICA 변경 가능")
    void testSetReplicaDataSourceContext() {
        RouteDataSourceContext.setReplica();
        assertThat(RouteDataSourceContext.getDataSourceType())
            .isEqualTo(DataSourceType.REPLICA);
    }
}
```

## 7.2 통합 테스트

```java
@SpringBootTest
class DataSourceRoutingIntegrationTest {
    
    @Autowired
    private UserService userService;
    
    @Test
    @DisplayName("사용자 생성 시 PRIMARY DataSource 사용")
    void testCreateUserUsesPrimary() {
        User user = User.builder()
            .name("김소울")
            .email("soul@example.com")
            .phone("010-1234-5678")
            .active(true)
            .build();
        
        User created = userService.createUser(user);
        assertThat(created.getId()).isNotNull();
    }
    
    @Test
    @DisplayName("사용자 조회 시 REPLICA DataSource 사용")
    void testGetUserUsesReplica() {
        // 먼저 사용자 생성
        User created = userService.createUser(user);
        
        // 조회 (REPLICA 사용)
        Optional<User> retrieved = userService.getUserById(created.getId());
        assertThat(retrieved).isPresent();
    }
}
```

## 7.3 성능 테스트

```java
@Test
@DisplayName("배치 INSERT 성능 측정")
void testBatchInsertPerformance() {
    long startTime = System.currentTimeMillis();
    
    List<User> users = new ArrayList<>();
    for (int i = 0; i < 1000; i++) {
        users.add(User.builder()
            .name("User" + i)
            .email("user" + i + "@example.com")
            .phone("010-0000-" + String.format("%04d", i))
            .active(true)
            .build());
    }
    
    userService.batchCreateUsers(users);
    
    long endTime = System.currentTimeMillis();
    long duration = endTime - startTime;
    
    System.out.println("배치 INSERT 1000개: " + duration + "ms");
    assertThat(duration).isLessThan(5000);  // 5초 이내
}
```

---

# 8. 실제 운영 환경 고려사항

## 8.1 데이터 동기화 지연 (Replication Lag)

```
Primary에 DATA 쓰기
    ↓
Replica에 전파되는 짧은 시간 동시성 문제 발생 가능
    ↓
Replica에서 READ 시 최신 데이터가 아닐 수 있음
```

**해결방안**:
```java
@Service
public class UserService {
    
    @Transactional
    public User createAndReturnUser(User user) {
        // 1. Primary에 INSERT
        User created = userRepository.save(user);
        
        // 2. 동기화를 기다리기 위해 약간의 로직 추가
        // (실제로는 Redis 캐시 등을 사용)
        
        // 3. Primary에서 재조회 (최신 데이터 보장)
        return userRepository.findById(created.getId())
            .orElseThrow();
    }
}
```

## 8.2 Primary 장애 처리

```java
@Service
public class FailoverUserService {
    
    @Transactional
    public User createUserWithFailover(User user) {
        try {
            // Primary 시도
            return userRepository.save(user);
        } catch (Exception e) {
            log.error("Primary 실패, Replica로 폴백 시도", e);
            
            // Replica에 쓰기 시도 (읽기 전용이므로 오류)
            throw new RuntimeException("쓰기 작업은 Primary만 가능", e);
        }
    }
}
```

## 8.3 모니터링

```java
@Component
public class DataSourceHealthMonitor {
    
    @Scheduled(fixedDelay = 60000)  // 1분마다
    public void checkDataSourceHealth() {
        try {
            Connection conn = dataSource.getConnection();
            Statement stmt = conn.createStatement();
            
            // Primary 확인
            stmt.executeQuery("SELECT 1");
            log.info("✓ Primary DataSource 정상");
            
            // Replica 확인
            RouteDataSourceContext.setReplica();
            stmt.executeQuery("SELECT 1");
            log.info("✓ Replica DataSource 정상");
            
        } catch (SQLException e) {
            log.error("✗ DataSource 오류: {}", e.getMessage());
            // 알람 발송
            notificationService.sendAlert("DB 연결 실패");
        } finally {
            RouteDataSourceContext.setPrimary();
        }
    }
}
```

---

# 9. MySQL Replication 실제 구성 예제

## 9.1 Docker Compose로 MySQL Primary-Replica 구성

```yaml
version: '3.8'
services:
  mysql-primary:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root_password
      MYSQL_DATABASE: app_db
    ports:
      - "3306:3306"
    volumes:
      - ./my-primary.cnf:/etc/mysql/my.cnf
    command: --server-id=1 --log-bin=mysql-bin --binlog-format=ROW
  
  mysql-replica:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root_password
    ports:
      - "3307:3306"
    depends_on:
      - mysql-primary
    command: --server-id=2 --relay-log=mysql-relay-bin
```

## 9.2 Replication 설정 스크립트

```bash
#!/bin/bash

# Primary에서 바이너리 로깅 상태 확인
mysql -h localhost -u root -p$MYSQL_ROOT_PASSWORD -e \
  "SHOW MASTER STATUS;" > master_status.txt

# Replica에 Replication 설정
mysql -h localhost -P 3307 -u root -p$MYSQL_ROOT_PASSWORD -e \
  "CHANGE REPLICATION SOURCE TO \
    SOURCE_HOST='mysql-primary', \
    SOURCE_USER='repl_user', \
    SOURCE_PASSWORD='repl_password', \
    SOURCE_LOG_FILE='mysql-bin.000001', \
    SOURCE_LOG_POS=154; \
   START REPLICA;"
```

---

# 10. 결론

## 10.1 정리

Spring Boot에서 Primary-Replica 데이터베이스 구성과 Transaction Routing을 구현하는 것은:

1. **AbstractRoutingDataSource** 활용
2. **AOP 포인트컷** 활용
3. **ThreadLocal 컨텍스트** 관리

이 세 가지 기술의 조합으로 가능합니다.

## 10.2 주요 이점

- ✅ **읽기 성능 향상**: 읽기를 여러 Replica로 분산
- ✅ **코드 간결화**: @ReadOnlyOnReplica 한 줄로 라우팅 제어
- ✅ **테스트 용이**: H2 메모리 DB로 간편한 테스트
- ✅ **확장성**: Replica 개수 쉽게 증가 가능

## 10.3 주의사항

- ⚠️ **Replication Lag**: 약간의 데이터 일관성 문제 가능
- ⚠️ **복잡성**: 장애 대응이 더 복잡할 수 있음
- ⚠️ **모니터링**: 지속적인건강 상태 확인 필요

## 10.4 다음 단계

이 패턴을 기반으로:
1. **읽기 전용 Replica 추가** (Primary 1개, Replica 3개+)
2. **자동 페일오버** (MHA, Orchestrator 등 사용)
3. **분산 트랜잭션** (MQ를 통한 이벤트 기반 동기화)
4. **캐시 계층 추가** (Redis, Memcached)

---

# 참고 자료

## 공식 문서
- [Spring Data JPA 공식 문서](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/){:target="_blank"}
- [Spring AOP 공식 문서](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html#aop){:target="_blank"}
- [AbstractRoutingDataSource API 문서](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jdbc/datasource/lookup/AbstractRoutingDataSource.html){:target="_blank"}

## 데이터베이스 복제
- [MySQL 공식 Replication 문서](https://dev.mysql.com/doc/refman/8.0/en/replication.html){:target="_blank"}
- [PostgreSQL 유류 복제 문서](https://www.postgresql.org/docs/current/warm-standby.html){:target="_blank"}
- [MariaDB Replication 가이드](https://mariadb.com/docs/reference/mdb/features/replication/){:target="_blank"}

## 관련 기술
- [H2 Database 공식 웹사이트](http://www.h2database.com/){:target="_blank"}
- [HikariCP 성능 및 설정 가이드](https://github.com/brettwooldridge/HikariCP){:target="_blank"}
- [Spring Transaction Management](https://docs.spring.io/spring-framework/docs/current/reference/html/data-access.html#transaction){:target="_blank"}

## 프로덕션 고려사항
- [MySQL 이중화 자동 페일오버 - MHA](https://github.com/yoshinorim/mha4mysql-manager){:target="_blank"}
- [Orchestrator - MySQL Replication 자동화](https://github.com/openark/orchestrator){:target="_blank"}
- [Redis를 이용한 캐싱 전략](https://redis.io/){:target="_blank"}

## 샘플 코드
- 이 글의 완전한 소스 코드는 아래에서 확인할 수 있습니다:
- [spring-boot-h2-replica 저장소](https://github.com/GracefulSoul/spring-boot-h2-replica){:target="_blank"}
