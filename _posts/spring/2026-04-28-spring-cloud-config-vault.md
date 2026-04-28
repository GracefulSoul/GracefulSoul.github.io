---
title: "Spring Cloud Config Server와 Vault 통합을 이용한 분산 설정 관리"
excerpt: "Spring Cloud Config Server와 HashiCorp Vault를 활용한 분산 환경에서의 안전한 설정 관리 방법을 학습합니다. 개념, 메커니즘, 차이점 및 실제 구현 예제를 포함합니다."
last_modified_at: 2026-04-28T10:00:00+09:00
header:
  image: /assets/images/spring/spring-cloud-config-vault.png
categories:
  - Spring
tags:
  - Programming
  - Spring
  - Spring Cloud
  - Config Server
  - Vault
  - 설정 관리
  - 마이크로서비스

toc: true
toc_ads: true
toc_sticky: true
---

## 개념 (Concept)

### Spring Cloud Config Server란?

**Spring Cloud Config Server**는 분산 시스템에서 설정 정보를 중앙에서 관리하고 제공하는 서버입니다. Git, SVN, 로컬 파일 시스템 등을 백엔드 저장소로 사용하여 여러 마이크로서비스의 설정을 버전 관리하고 동적으로 업데이트할 수 있습니다.

**주요 특징:**
- 중앙 집중식 설정 관리
- Git 기반 버전 관리
- 환경별(dev, prod) 설정 분리
- 실시간 설정 업데이트
- RESTful API를 통한 설정 조회

### HashiCorp Vault란?

**HashiCorp Vault**는 민감한 정보를 안전하게 저장, 관리, 접근하기 위한 도구입니다. 데이터베이스 패스워드, API 키, 토큰, 인증서 등을 암호화하여 저장하고 감사 로그를 기록합니다.

**주요 특징:**
- 암호화된 저장소
- 다양한 인증 방식 지원
- 자동 인증서 관리
- 비밀 로테이션
- 감사 로그 기록

---

## 메커니즘 (Mechanism)

### Spring Cloud Config Server 동작 원리

```
┌─────────────────────────────────────────────────────────┐
│                    Client Application                   │
│  ┌─────────────────────────────────────────────────┐    │
│  │   bootstrap.yml                                 │    │
│  │   - Config Server URI 설정                       │    │
│  │   - Vault 연결 정보                              │    │
│  └─────────────────────────────────────────────────┘    │
└──────────────────────┬──────────────────────────────────┘
                       │ (1) 시작 시 Config Server 연결
                       ▼
        ┌──────────────────────────────┐
        │   Config Server              │
        │  (Port: 8888)                │
        │  ┌────────────────────────┐  │
        │  │ Git Repository         │  │
        │  │ ├─ client-app.yml      │  │
        │  │ ├─ client-app-dev.yml  │  │
        │  │ └─ client-app-prod.yml │  │
        │  └────────────────────────┘  │
        └──────────────────────────────┘
                       │ (2) 설정 파일 제공
                       ▼
        ┌──────────────────────────────┐
        │      Vault Server            │
        │     (Port: 8200)             │
        │  ┌────────────────────────┐  │
        │  │ Secret Storage         │  │
        │  │ ├─ database/username   │  │
        │  │ ├─ database/password   │  │
        │  │ ├─ jwt-secret          │  │
        │  │ └─ api-key             │  │
        │  └────────────────────────┘  │
        └──────────────────────────────┘
                       │ (3) 민감한 정보 제공
                       ▼
        Client Application (실행 시작)
```

### 설정 로드 순서

1. **Bootstrap Phase (부트스트랩 단계)**
   - `bootstrap.yml` 로드 (Config Server/Vault 연결 정보)
   - Config Server에서 설정 파일 다운로드
   - Vault에서 민감한 정보 조회

2. **Application Phase (애플리케이션 단계)**
   - `application.yml` 로드 (기본 설정)
   - 환경 변수 적용
   - 스프링 부트 초기화

---

## 내부 구조 (Architecture)

### Config Server 내부 동작

```java
// 1. Config Server 시작
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}

// 2. Config Server 설정
// application.yml
spring:
  cloud:
    config:
      server:
        git:
          uri: file:${java.io.tmpdir}/spring-cloud-config-repo
          clone-on-start: true
          search-paths: '{application}'

// 3. 클라이언트의 설정 요청
// GET /client-app/prod
// 응답:
// {
//   "name": "client-app",
//   "profiles": ["prod"],
//   "label": "master",
//   "version": "abc1234",
//   "state": null,
//   "propertySources": [...]
// }
```

### Vault 통합 아키텍처

```
┌────────────────────────────────────────────────┐
│         Spring Cloud Vault                     │
│  ┌──────────────────────────────────────────┐  │
│  │  VaultTemplate                           │  │
│  │  ├─ readSecrets()                        │  │
│  │  ├─ write()                              │  │
│  │  └─ opsForKeyValue()                     │  │
│  └──────────────────────────────────────────┘  │
└────────────────────┬───────────────────────────┘
                     │
        ┌────────────▼─────────────┐
        │   Authentication         │
        │  ┌────────────────────┐  │
        │  │ Token              │  │
        │  │ AppRole            │  │
        │  │ Kubernetes         │  │
        │  │ LDAP/Okta          │  │
        │  └────────────────────┘  │
        └──────────────────────────┘
                     │
        ┌────────────▼─────────────┐
        │   Vault Server           │
        │  ┌────────────────────┐  │
        │  │ Secret Engines     │  │
        │  │ ├─ KV v2           │  │
        │  │ ├─ Database        │  │
        │  │ ├─ PKI             │  │
        │  │ └─ Transit         │  │
        │  └────────────────────┘  │
        └──────────────────────────┘
```

### 속성 주입 메커니즘

```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    // Config Server + Vault → Spring Environment → AppProperties
    private String name;           // application.yml에서
    private Database database;     // Config Server에서
    private Security security;     // Vault에서
}

@RestController
public class ConfigController {
    // 방법 1: @Value 애노테이션
    @Value("${app.name}")
    private String appName;
    
    // 방법 2: @ConfigurationProperties 클래스 주입
    @Autowired
    private AppProperties appProperties;
    
    // 방법 3: Environment 객체 사용
    @Autowired
    private Environment environment;
}
```

---

## Spring Cloud Config Server vs Vault 차이점

| 항목 | Config Server | Vault |
|:-----|:---|:---|
| **목적** | 애플리케이션 설정 관리 | 민감한 정보 관리 |
| **저장소** | Git, SVN, 파일 시스템 | 암호화된 메모리 저장소 |
| **데이터 타입** | 설정값 전체 | 민감한 정보 (암호, 토큰) |
| **버전 관리** | Git 기반 버전 관리 | 버전 지원하지 않음 |
| **감시** | 변경 이력 조회 가능 | 감사 로그 기록 |
| **보안** | 저장소 수준의 보안 | 암호화 + 접근 제어 |
| **동적 업데이트** | 지원 (Config Client) | 제한적 |
| **확장성** | 좋음 | 높음 |
| **사용 사례** | 애플리케이션 설정 | API 키, DB 패스, 인증서 |

---

## 장점과 단점

### Spring Cloud Config Server

**장점:**
- 중앙 집중식 설정 관리로 일관성 유지
- Git 기반 버전 관리 및 감시
- 환경별 설정 분리 용이
- 변경 이력 추적 가능
- RESTful API 제공
- 동적 설정 업데이트 지원

**단점:**
- 민감한 정보는 평문으로 저장되므로 추가 보안 필요
- Config Server 가용성 영향도가 큼
- 네트워크 지연 가능성
- Git 저장소 관리 필요

### HashiCorp Vault

**장점:**
- 암호화된 저장소로 높은 보안
- 다양한 인증 방식 지원
- 자동 인증서 관리
- 감사 로그 기록
- 비밀 로테이션 지원
- 고가용성 클러스터 지원

**단점:**
- 추가 서비스 운영 필요
- 러닝 커브가 높음
- Config Server와 별도로 구성 필요
- 성능 오버헤드 가능

---

## 활용 샘플

### 1. 프로젝트 구조

```
spring-cloud-config-vault/                    # 부모 프로젝트 (Multi-Module)
├── pom.xml                                   # 부모 POM (의존성 관리)
├── config-server/                            # Config Server 모듈
│   ├── pom.xml
│   └── src/main/java
│       └── com/example/configserver/
│           └── ConfigServerApplication.java
├── client-app/                               # Client Application 모듈
│   ├── pom.xml
│   └── src/main/java
│       └── com/example/clientapp/
│           ├── ClientAppApplication.java
│           ├── config/AppProperties.java
│           └── controller/ConfigController.java
└── vault-config/                             # Vault 설정 및 스크립트
    └── init-vault.ps1
```

### 2. Vault 초기화 (PowerShell)

```powershell
# Vault 서버 시작 (개발 모드)
vault server -dev

# 데이터베이스 자격증명 저장
vault kv put secret/data/client-app/database `
    username="dbuser" `
    password="db-secure-password-2024" `
    url="jdbc:postgresql://localhost:5432/client_db" `
    maxPoolSize=20

# 보안 설정 저장
vault kv put secret/data/client-app/security `
    jwtSecret="vault-managed-jwt-secret-key" `
    jwtExpiration=86400000 `
    apiKey="vault-managed-api-key"
```

### 3. Config Server 설정

```yaml
# config-server/src/main/resources/application.yml
spring:
  application:
    name: config-server
  cloud:
    config:
      server:
        git:
          uri: file:${java.io.tmpdir}/spring-cloud-config-repo
          clone-on-start: true
          search-paths: '{application}'

server:
  port: 8888
```

### 4. Client Application 설정

```yaml
# client-app/src/main/resources/bootstrap.yml
spring:
  application:
    name: client-app
  cloud:
    config:
      uri: http://localhost:8888
      fail-fast: true
    vault:
      enabled: true
      host: localhost
      port: 8200
      scheme: http
      authentication: TOKEN
      token: s.xxxxxxxxxxxxxxxx
      kv:
        enabled: true
        backend: secret
        version: 2
```

```yaml
# client-app/src/main/resources/application.yml
spring:
  application:
    name: client-app

server:
  port: 8080

app:
  name: Client Application
  version: 1.0.0
  environment: development
  database:
    url: jdbc:postgresql://localhost:5432/myapp_db
    username: appuser
    password: password123
    max-pool-size: 10
  security:
    jwt-secret: ${vault:secret/data/client-app/security/jwtSecret}
    jwt-expiration: 86400000
    api-key: ${vault:secret/data/client-app/security/apiKey}
```

### 5. 환경별 설정 파일

```yaml
# vault-config/client-app.yml (공통 설정)
spring:
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false

app:
  name: Client Application
  version: 1.0.0
  environment: ${ENVIRONMENT:development}
```

```yaml
# vault-config/client-app-dev.yml (개발 환경)
spring:
  jpa:
    hibernate:
      ddl-auto: create-drop
    show-sql: true

app:
  environment: development
  database:
    url: jdbc:postgresql://localhost:5432/myapp_dev
    max-pool-size: 5

logging:
  level:
    root: DEBUG
    com.example: DEBUG
```

```yaml
# vault-config/client-app-prod.yml (프로덕션 환경)
spring:
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false

app:
  environment: production
  database:
    url: jdbc:postgresql://prod-db.example.com:5432/myapp_prod
    max-pool-size: 20

logging:
  level:
    root: WARN
```

---

## 주요 코드 설명

### 1. Config Server 활성화

```java
// config-server/src/main/java/com/example/configserver/ConfigServerApplication.java
@SpringBootApplication
@EnableConfigServer      // Config Server 기능 활성화
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

`@EnableConfigServer` 애노테이션은 다음을 자동 설정합니다:
- EnvironmentController: 설정 조회 엔드포인트
- ResourceRepository: Git/파일 시스템 접근
- EnvironmentRepository: 설정 데이터 관리

### 2. @ConfigurationProperties 클래스

```java
// client-app/src/main/java/com/example/clientapp/config/AppProperties.java
@Component
@ConfigurationProperties(prefix = "app")
@Data  // Lombok: getter, setter, toString, equals, hashCode 자동 생성
public class AppProperties {
    
    private String name;
    private String version;
    private String environment;
    
    private Database database = new Database();
    private Security security = new Security();

    @Data
    public static class Database {
        private String url;
        private String username;
        private String password;
        private int maxPoolSize;
    }

    @Data
    public static class Security {
        private String jwtSecret;
        private long jwtExpiration;
        private String apiKey;
    }
}
```

로드 흐름:
```
Vault: secret/data/client-app/security → Spring Environment
                                              ↓
                            @ConfigurationProperties 처리
                                              ↓
                            AppProperties.security 필드 값 설정
```

### 3. Controller에서 설정 사용

```java
// client-app/src/main/java/com/example/clientapp/controller/ConfigController.java
@RestController
@RequestMapping("/api/config")
@RequiredArgsConstructor  // Lombok: final 필드 생성자 자동 생성
public class ConfigController {

    private final AppProperties appProperties;

    // 방법 1: @Value 애노테이션
    @Value("${app.name:Not Set}")
    private String appName;

    @Value("${app.version:Not Set}")
    private String appVersion;

    // 방법 2: @ConfigurationProperties 주입
    @GetMapping("/properties")
    public ResponseEntity<Map<String, Object>> getProperties() {
        Map<String, Object> response = new HashMap<>();
        
        Map<String, Object> app = new HashMap<>();
        app.put("name", appProperties.getName());
        app.put("version", appProperties.getVersion());
        app.put("environment", appProperties.getEnvironment());
        
        Map<String, Object> database = new HashMap<>();
        database.put("url", appProperties.getDatabase().getUrl());
        database.put("username", appProperties.getDatabase().getUsername());
        database.put("maxPoolSize", appProperties.getDatabase().getMaxPoolSize());
        
        Map<String, Object> security = new HashMap<>();
        security.put("jwtExpiration", appProperties.getSecurity().getJwtExpiration());
        // 민감한 정보는 존재 여부만 확인
        security.put("apiKeyExists", 
            appProperties.getSecurity().getApiKey() != null && 
            !appProperties.getSecurity().getApiKey().isEmpty());
        
        response.put("app", app);
        response.put("database", database);
        response.put("security", security);
        
        return ResponseEntity.ok(response);
    }

    @GetMapping("/status")
    public ResponseEntity<Map<String, String>> getStatus() {
        Map<String, String> response = new HashMap<>();
        response.put("status", "UP");
        response.put("appName", appName);
        response.put("appVersion", appVersion);
        
        return ResponseEntity.ok(response);
    }
}
```

### 4. Vault에서 설정 로드 (bootstrap.yml)

```yaml
spring:
  application:
    name: client-app
  
  cloud:
    # Config Server 설정
    config:
      uri: http://localhost:8888
      fail-fast: true
      retry:
        initial-interval: 1000
        max-interval: 2000
        max-attempts: 6
    
    # Vault 설정
    vault:
      enabled: true
      host: localhost
      port: 8200
      scheme: http
      
      # 인증 방식
      authentication: TOKEN
      token: s.xxxxxxxxxxxxxxxx
      
      # KV v2 Secret Engine
      kv:
        enabled: true
        backend: secret
        version: 2
        profile-separator: '/'
```

경로 매핑:
```
Vault 경로: secret/data/client-app/security/jwtSecret
매핑된 속성: app.security.jwt-secret (kebab-case로 자동 변환)
```

### 5. 환경 변수 사용

```java
// 환경 변수 설정
System.setProperty("ENVIRONMENT", "production");
System.setProperty("DATABASE_URL", "jdbc:postgresql://prod-db:5432/db");

// application.yml에서 사용
app:
  environment: ${ENVIRONMENT:development}
  database:
    url: ${DATABASE_URL:jdbc:postgresql://localhost:5432/db}
```

---

## 실행 방법

### 1. Vault 시작 (개발 모드)

```bash
vault server -dev
# 출력: Unseal Key: ...
#       Root Token: s.xxxxxxxxxxxxx
```

### 2. Vault 초기화

PowerShell 스크립트 실행:
```powershell
cd vault-config
.\init-vault.ps1
```

### 3. Config Server 실행

```bash
cd config-server
mvn spring-boot:run
# 또는
mvn clean install
java -jar target/spring-cloud-config-server-1.0.0.jar
```

### 4. Client Application 실행

```bash
cd client-app
mvn spring-boot:run
# 또는
java -jar target/spring-cloud-config-client-app-1.0.0.jar
```

### 5. API 호출

```bash
# 설정 확인
curl http://localhost:8080/api/config/properties

# 상태 확인
curl http://localhost:8080/api/config/status

# Actuator Endpoint
curl http://localhost:8080/actuator/configprops
curl http://localhost:8080/actuator/env
```

---

## Best Practices (모범 사례)

### 1. Config Server 구성

```yaml
# 개발 환경에서는 로컬 파일 시스템 사용
spring:
  cloud:
    config:
      server:
        git:
          uri: file:/tmp/config-repo

# 프로덕션 환경에서는 원격 Git 저장소 사용
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/org/config-repo
          username: ${GIT_USERNAME}
          password: ${GIT_PASSWORD}
```

### 2. Vault 인증 방식 선택

```yaml
# 개발 환경: Token 기반
vault:
  authentication: TOKEN
  token: s.xxxxxxxxxxxxx

# 프로덕션 환경: AppRole 기반
vault:
  authentication: APPROLE
  app-role:
    role-id: ${VAULT_ROLE_ID}
    secret-id: ${VAULT_SECRET_ID}

# Kubernetes 환경: Kubernetes 인증
vault:
  authentication: KUBERNETES
  kubernetes:
    role: client-app
```

### 3. 민감한 정보 관리

```yaml
# Vault에만 저장할 정보
app:
  security:
    jwt-secret: ${vault:secret/data/client-app/security/jwtSecret}
    api-key: ${vault:secret/data/client-app/security/apiKey}
    db-password: ${vault:secret/data/client-app/database/password}

# Config Server에 저장 가능한 정보
app:
  name: My Application
  version: 1.0.0
  logging:
    level: INFO
```

### 4. 설정 검증

```java
@Component
@ConfigurationProperties(prefix = "app")
@Validated  // 유효성 검증 활성화
public class AppProperties {
    
    @NotNull(message = "Application name must not be null")
    @NotBlank(message = "Application name must not be blank")
    private String name;
    
    @NotNull
    private String version;
    
    @Valid  // 중첩된 객체 검증
    private Database database = new Database();
    
    @Data
    public static class Database {
        @NotNull
        @Pattern(regexp = "jdbc:.*", message = "Invalid JDBC URL")
        private String url;
        
        @NotNull
        @Min(1)
        @Max(100)
        private int maxPoolSize;
    }
}
```

---

## 문제 해결

### Config Server에 연결할 수 없음

```bash
# 문제: Connection refused
# 해결:
1. Config Server 실행 확인: curl http://localhost:8888/actuator/health
2. bootstrap.yml의 spring.cloud.config.uri 확인
3. fail-fast 설정 확인: false로 변경하면 서버 시작 안 함
```

### Vault에서 비밀을 로드할 수 없음

```bash
# 문제: 403 Forbidden
# 해결:
1. Token 유효성 확인: vault token lookup
2. Token 권한 확인: vault token lookup -self
3. 경로 확인: vault kv list secret/data/client-app

# 권한 설정 예
vault policy write client-app - <<EOF
path "secret/data/client-app/*" {
  capabilities = ["read", "list"]
}
EOF

vault token create -policy=client-app
```

### 설정이 업데이트되지 않음

```bash
# 문제: 설정 변경 후 적용 안 됨
# 해결:

# 1. Actuator refresh 엔드포인트 활용
curl -X POST http://localhost:8080/actuator/refresh

# 2. @RefreshScope 애노테이션 사용
@Component
@RefreshScope  // 설정 변경 시 자동 갱신
public class DynamicConfig {
    @Value("${app.name}")
    private String appName;
}

# 3. 애플리케이션 재시작
```

---

## 참고자료

- [Spring Cloud Config 공식 문서](https://spring.io/projects/spring-cloud-config){:target="_blank"}
- [Spring Cloud Vault 공식 문서](https://spring.io/projects/spring-cloud-vault){:target="_blank"}
- [HashiCorp Vault 공식 문서](https://www.vaultproject.io/docs){:target="_blank"}
- [Spring Boot 설정 바인딩](https://spring.io/guides/tutorials/spring-boot-kotlin/){:target="_blank"}
- [Spring Cloud Config Server 가이드](https://cloud.spring.io/spring-cloud-config/reference/html/){:target="_blank"}
- [Vault 비밀 관리](https://learn.hashicorp.com/collections/vault/secrets-management){:target="_blank"}
- [샘플 프로젝트 GitHub](https://github.com/GracefulSoul/spring-cloud-config-vault){:target="_blank"}

---

## 소스코드

샘플 코드는 [여기](https://github.com/GracefulSoul/spring-cloud-config-vault){:target="_blank"}에서 확인 가능합니다.
