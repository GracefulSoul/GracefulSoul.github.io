---
title: "데이터 동시성 제어 - 낙관락, 비관락, 분산락 (Java/Spring)"
excerpt: "Java와 Spring을 사용한 데이터 동시성 제어. 낙관락(Optimistic Locking), 비관락(Pessimistic Locking), 분산락(Distributed Lock)의 개념, 메커니즘, 구현 방법을 상세히 설명합니다."
last_modified_at: 2026-04-18T15:30:00+09:00
header:
  image: /assets/images/database/data-concurrency-lock.png
categories:
  - Database
tags:
  - Programming
  - Database
  - Concurrency
  - Lock
  - Java
  - Spring
  - JPA

toc: true
toc_ads: true
toc_sticky: true
---

# 개요

멀티스레드 또는 분산 환경에서 동시에 같은 데이터에 접근할 때 데이터 일관성을 보장하는 것은 매우 중요합니다. 
본 글에서는 Java/Spring 환경에서 사용되는 대표적인 동시성 제어 메커니즘인 **낙관락(Optimistic Locking)**, 
**비관락(Pessimistic Locking)**, **분산락(Distributed Lock)**을 심층 분석하고 실제 샘플 코드로 구현합니다.

---

# 1. 동시성 문제와 데이터 일관성

## 1.1 동시성 문제 유형

데이터베이스에서 발생할 수 있는 주요 동시성 문제:

| 문제 | 설명 | 시나리오 |
|------|------|--------|
| **Lost Update(손실된 업데이트)** | 두 트랜잭션이 같은 데이터를 수정하면 마지막 쓰기만 반영 | A, B가 동시에 계좌 잔액 수정 |
| **Dirty Read(더티 읽기)** | 커밋되지 않은 데이터를 다른 트랜잭션이 읽음 | 롤백된 데이터를 읽음 |
| **Non-repeatable Read** | 트랜잭션 중 같은 데이터를 여러 번 읽을 때 값이 달라짐 | 트랜잭션 진행 중 다른 트랜잭션이 데이터 수정 |
| **Phantom Read** | 트랜잭션 중 새로운 행이 추가/삭제되어 조회 결과가 달라짐 | 범위 조회 중 새로운 행 삽입 |

```
[타임라인 예시: Lost Update 문제]

시간    | 트랜잭션 A              | 트랜잭션 B
--------|----------------------|----------------------
T1      | 읽기: 잔액 = 10,000   |
T2      |                      | 읽기: 잔액 = 10,000
T3      | 쓰기: 10,000 - 5,000  |
T4      | COMMIT               |
T5      |                      | 쓰기: 10,000 + 3,000
T6      |                      | COMMIT
--------|----------------------|----------------------
결과    | 최종 잔액 = 13,000 (A의 출금 5,000은 반영 안됨!)
```

---

# 2. 낙관락(Optimistic Locking)

## 2.1 개념 및 원리

**낙관락**은 대부분의 데이터 충돌이 드물다고 가정하고, 충돌이 발생하면 그때 처리하는 방식입니다.

### 동작 원리

```
1. 데이터 조회 시 버전(Version) 값 함께 읽음
2. 비즈니스 로직 처리 (락 없음)
3. 업데이트 시 버전값으로 충돌 검사
   UPDATE table SET col = value, version = version + 1
   WHERE id = ? AND version = ?
4. 버전 불일치 → ObjectOptimisticLockingFailureException
5. 재시도(Retry) 메커니즘으로 복구
```

## 2.2 내부 구조

### 버전 필드(Version Field) 메커니즘

JPA의 `@Version` 애노테이션을 사용하면 다음과 같은 동작:

```
[초기 상태]
ID | ACCOUNT_NUMBER | BALANCE | VERSION
1  | ACC-001        | 10,000  | 1

[첫 번째 업데이트 후]
ID | ACCOUNT_NUMBER | BALANCE | VERSION
1  | ACC-001        | 5,000   | 2  ← 자동 증가

[동시 업데이트 시도]
UPDATE account SET balance = 8000, version = 3 WHERE id = 1 AND version = 1
→ 0 rows updated (version = 2, 1이 아님)
→ OptimisticLockingFailureException 발생
```

## 2.3 구현 예제

### 엔티티 정의

```java
@Entity
@Table(name = "optimistic_account")
@Getter @Setter @NoArgsConstructor
public class OptimisticAccount {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String accountNumber;
    
    @Column(nullable = false)
    private Long balance;
    
    /**
     * @Version: 낙관락의 핵심
     * - JPA가 자동으로 관리
     * - 엔티티 업데이트마다 증가
     * - WHERE 절에 포함되어 동시성 충돌 감지
     */
    @Version
    private Long version;
    
    public void withdraw(Long amount) {
        if (balance < amount) {
            throw new IllegalArgumentException("잔액이 부족합니다");
        }
        this.balance -= amount;
    }
    
    public void deposit(Long amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("입금액은 0보다 커야 합니다");
        }
        this.balance += amount;
    }
}
```

### 저장소(Repository)

```java
@Repository
public interface OptimisticAccountRepository 
    extends JpaRepository<OptimisticAccount, Long> {
    
    Optional<OptimisticAccount> findByAccountNumber(String accountNumber);
    
    /**
     * 낙관락을 명시적으로 적용
     * LockModeType.OPTIMISTIC: 버전 필드만 체크
     * LockModeType.OPTIMISTIC_FORCE_INCREMENT: 버전 증가만 함
     */
    @Lock(LockModeType.OPTIMISTIC)
    @Query("SELECT a FROM OptimisticAccount a WHERE a.accountNumber = :accountNumber")
    Optional<OptimisticAccount> findByAccountNumberWithOptimisticLock(
        @Param("accountNumber") String accountNumber);
}
```

### 서비스 구현

```java
@Service
@RequiredArgsConstructor
@Slf4j
public class OptimisticLockService {
    
    private final OptimisticAccountRepository accountRepository;
    private static final int MAX_RETRY_COUNT = 3;
    
    @Transactional
    public void transfer(String fromAccountNumber, String toAccountNumber, Long amount) {
        int retryCount = 0;
        
        while (retryCount < MAX_RETRY_COUNT) {
            try {
                OptimisticAccount fromAccount = accountRepository
                    .findByAccountNumberWithOptimisticLock(fromAccountNumber)
                    .orElseThrow(() -> new IllegalArgumentException("계좌를 찾을 수 없습니다"));
                
                OptimisticAccount toAccount = accountRepository
                    .findByAccountNumberWithOptimisticLock(toAccountNumber)
                    .orElseThrow(() -> new IllegalArgumentException("계좌를 찾을 수 없습니다"));
                
                // 비즈니스 로직 처리 (락 없음)
                fromAccount.withdraw(amount);
                toAccount.deposit(amount);
                
                // 저장 시 버전 체크
                accountRepository.save(fromAccount);
                accountRepository.save(toAccount);
                
                log.info("이체 완료: {} → {}, 금액: {}", 
                    fromAccountNumber, toAccountNumber, amount);
                return;
                
            } catch (ObjectOptimisticLockingFailureException e) {
                retryCount++;
                log.warn("낙관락 충돌! 재시도 {}/{}", retryCount, MAX_RETRY_COUNT);
                
                if (retryCount >= MAX_RETRY_COUNT) {
                    throw new RuntimeException("최대 재시도 횟수 초과", e);
                }
            }
        }
    }
}
```

## 2.4 생성되는 SQL

```sql
-- 조회
SELECT * FROM optimistic_account WHERE account_number = ? FOR UPDATE;

-- 업데이트 (버전 체크)
UPDATE optimistic_account 
SET balance = ?, version = version + 1 
WHERE id = ? AND version = ?;
```

## 2.5 특징

| 항목 | 설명 |
|------|-----|
| **장점** | • 충돌 빈도 낮을 때 성능 우수<br>• DB 락 없어 동시성 높음<br>• 데드락 위험 없음 |
| **단점** | • 충돌 시 Exception 처리<br>• 재시도 로직 구현 필요<br>• 충돌 빈번하면 성능 저하 |
| **사용 시기** | • 조회 > 수정 작업<br>• 충돌 가능성 낮음<br>• 높은 동시성 필요 시 |

---

# 3. 비관락(Pessimistic Locking)

## 3.1 개념 및 원리

**비관락**은 데이터 충돌이 자주 발생한다고 가정하고, 미리 행을 잠금하는 방식입니다.

### 동작 원리

```
1. 데이터 조회 시 즉시 행 잠금 획득
   SELECT ... FOR UPDATE (배타락) 또는 
   SELECT ... FOR UPDATE SHARED (공유락)
2. 다른 트랜잭션의 접근 차단
3. 비즈니스 로직 처리
4. 업데이트 수행
5. 트랜잭션 종료 시 잠금 자동 해제
```

## 3.2 내부 구조

### 락 모드 타입

```
┌─ PESSIMISTIC_READ (공유락, Shared Lock)
│  • SELECT ... FOR UPDATE SHARED
│  • 다른 공유락 허용, 배타락 차단
│  • 읽기 전용 작업 시 사용
│
└─ PESSIMISTIC_WRITE (배타락, Exclusive Lock)
   • SELECT ... FOR UPDATE
   • 모든 다른 락 차단
   • 수정 작업 시 사용
```

### 잠금 대기 흐름

```
[시간 흐름]

스레드 A                          스레드 B
─────────────────────────────────────────────────
SELECT ... FOR UPDATE
(배타락 획득) ✓
  ↓
비즈니스 로직 처리 (1초)
  ↓                            SELECT ... FOR UPDATE
  ↓                            (대기 중...)
UPDATE 수행
COMMIT (락 해제)
  ↓                            (배타락 획득) ✓
  ↓                            비즈니스 로직 처리
  ↓                            UPDATE 수행
  ↓                            COMMIT
완료                           완료
```

## 3.3 구현 예제

### 저장소(Repository)

```java
@Repository
public interface PessimisticAccountRepository 
    extends JpaRepository<PessimisticAccount, Long> {
    
    Optional<PessimisticAccount> findByAccountNumber(String accountNumber);
    
    /**
     * 배타락(PESSIMISTIC_WRITE)
     * 생성되는 SQL: SELECT ... FOR UPDATE
     */
    @Lock(LockModeType.PESSIMISTIC_WRITE)
    @Query("SELECT a FROM PessimisticAccount a WHERE a.accountNumber = :accountNumber")
    Optional<PessimisticAccount> findByAccountNumberWithPessimisticWriteLock(
        @Param("accountNumber") String accountNumber);
    
    /**
     * 공유락(PESSIMISTIC_READ)
     * 생성되는 SQL: SELECT ... FOR UPDATE SHARED (지원하는 DB의 경우)
     */
    @Lock(LockModeType.PESSIMISTIC_READ)
    @Query("SELECT a FROM PessimisticAccount a WHERE a.accountNumber = :accountNumber")
    Optional<PessimisticAccount> findByAccountNumberWithPessimisticReadLock(
        @Param("accountNumber") String accountNumber);
}
```

### 서비스 구현

```java
@Service
@RequiredArgsConstructor
@Slf4j
public class PessimisticLockService {
    
    private final PessimisticAccountRepository accountRepository;
    
    /**
     * 배타락 기반 이체
     * - 두 계좌 모두 배타락 획득
     * - 다른 트랜잭션의 모든 접근 차단
     */
    @Transactional
    public void transfer(String fromAccountNumber, String toAccountNumber, Long amount) {
        // 데드락 방지: 계좌번호 기준으로 일관된 순서로 획득
        PessimisticAccount fromAccount = accountRepository
            .findByAccountNumberWithPessimisticWriteLock(fromAccountNumber)
            .orElseThrow(() -> new IllegalArgumentException("계좌를 찾을 수 없습니다"));
        
        PessimisticAccount toAccount = accountRepository
            .findByAccountNumberWithPessimisticWriteLock(toAccountNumber)
            .orElseThrow(() -> new IllegalArgumentException("계좌를 찾을 수 없습니다"));
        
        // 이미 배타락을 획득했으므로 안전하게 처리
        fromAccount.withdraw(amount);
        toAccount.deposit(amount);
        
        accountRepository.save(fromAccount);
        accountRepository.save(toAccount);
        
        log.info("이체 완료: {} → {}", fromAccountNumber, toAccountNumber);
    }
    
    /**
     * 공유락 기반 잔액 조회
     * - 읽기 전용 작업
     * - 다른 공유락은 허용, 배타락만 차단
     */
    @Transactional(readOnly = true)
    public Long getBalance(String accountNumber) {
        PessimisticAccount account = accountRepository
            .findByAccountNumberWithPessimisticReadLock(accountNumber)
            .orElseThrow(() -> new IllegalArgumentException("계좌를 찾을 수 없습니다"));
        
        return account.getBalance();
    }
}
```

## 3.4 생성되는 SQL

```sql
-- 배타락 (PESSIMISTIC_WRITE)
SELECT * FROM pessimistic_account 
WHERE account_number = ? FOR UPDATE;

-- 공유락 (PESSIMISTIC_READ)
SELECT * FROM pessimistic_account 
WHERE account_number = ? FOR UPDATE SHARED;

-- 업데이트 (일반 UPDATE, 잠금 이미 획득)
UPDATE pessimistic_account 
SET balance = ? 
WHERE id = ?;
```

## 3.5 데드락(Deadlock) 방지

```java
/**
 * 데드락 발생 상황
 * [시간]  [트랜잭션 A]        [트랜잭션 B]
 * T1      Lock(ACC-001)
 * T2                         Lock(ACC-002)
 * T3      Lock(ACC-002)← 대기 (ACC-002는 B가 소유)
 * T4      
 * T5                         Lock(ACC-001)← 대기 (ACC-001은 A가 소유)
 * ↓       DEADLOCK 발생!
 * 
 * 해결: 항상 일관된 순서로 잠금 획득
 */

@Transactional
public void transferSafely(String from, String to, Long amount) {
    // 계좌번호를 정렬하여 항상 같은 순서로 획득
    String[] sorted = {from, to};
    java.util.Arrays.sort(sorted);
    
    PessimisticAccount account1 = accountRepository
        .findByAccountNumberWithPessimisticWriteLock(sorted[0])
        .get();
    
    PessimisticAccount account2 = accountRepository
        .findByAccountNumberWithPessimisticWriteLock(sorted[1])
        .get();
    
    // 안전하게 처리
}
```

## 3.6 특징

| 항목 | 설명 |
|------|-----|
| **장점** | • 충돌 자주 발생할 때 성능 우수<br>• 명시적인 잠금으로 데이터 일관성 보장<br>• 재시도 로직 불필요 |
| **단점** | • DB 잠금으로 동시성 감소<br>• 데드락 위험 존재<br>• 락 대기로 응답 지연 가능 |
| **사용 시기** | • 충돌 자주 발생<br>• 데이터 일관성 중요<br>• 트랜잭션 짧음 |

---

# 4. 분산락(Distributed Lock)

## 4.1 개념 및 원리

**분산락**은 마이크로서비스나 다중 인스턴스 환경에서 여러 서버에 걸쳐 동시성을 제어하는 방식입니다.
일반적으로 Redis, Zookeeper 등의 외부 저장소를 사용합니다.

### 동작 원리

```
1. 외부 저장소(Redis)에서 락 획득 시도
2. 락 획득 성공 여부 즉시 반환
3. 락 획득 시 비즈니스 로직 처리
4. 로직 완료 후 락 해제
5. 락 획득 실패 시 재시도 또는 에러 처리
```

## 4.2 구현 방식

### Redisson을 사용한 분산락

Redisson은 Redis 기반의 분산락을 제공하는 라이브러리입니다.

#### 설정

```java
@Configuration
public class RedissonConfig {
    
    @Bean
    public RedissonClient redissonClient() {
        Config config = new Config();
        config.useSingleServer()
            .setAddress("redis://localhost:6379")
            .setConnectionPoolSize(64)
            .setConnectionMinimumIdleSize(10)
            .setRetryAttempts(3)
            .setRetryInterval(1500);
        
        return Redisson.create(config);
    }
}
```

## 4.3 구현 예제

### 분산락 서비스

```java
@Service
@RequiredArgsConstructor
@Slf4j
public class DistributedLockService {
    
    private final DistributedAccountRepository accountRepository;
    private final RedissonClient redissonClient;
    
    private static final long LOCK_WAIT_TIME = 10;   // 초
    private static final long LOCK_LEASE_TIME = 3;   // 초
    private static final TimeUnit TIME_UNIT = TimeUnit.SECONDS;
    
    /**
     * 분산락 기반 이체
     * - Redis를 사용한 다중 서버 환경의 동시성 제어
     */
    @Transactional
    public void transfer(String fromAccountNumber, String toAccountNumber, Long amount) {
        // 데드락 방지: 정렬된 순서로 락 획득
        String[] accounts = {fromAccountNumber, toAccountNumber};
        java.util.Arrays.sort(accounts);
        
        RLock lock1 = redissonClient.getLock("account-lock:" + accounts[0]);
        RLock lock2 = redissonClient.getLock("account-lock:" + accounts[1]);
        
        try {
            // 첫 번째 락 획득 (10초 대기, 3초 자동 해제)
            boolean lock1Acquired = lock1.tryLock(
                LOCK_WAIT_TIME, LOCK_LEASE_TIME, TIME_UNIT);
            
            if (!lock1Acquired) {
                throw new RuntimeException("첫 번째 락 획득 실패");
            }
            
            // 두 번째 락 획득
            boolean lock2Acquired = lock2.tryLock(
                LOCK_WAIT_TIME, LOCK_LEASE_TIME, TIME_UNIT);
            
            if (!lock2Acquired) {
                throw new RuntimeException("두 번째 락 획득 실패");
            }
            
            try {
                // 락 획득 후 DB 조회 및 업데이트
                DistributedAccount fromAccount = accountRepository
                    .findByAccountNumber(fromAccountNumber)
                    .orElseThrow(() -> new IllegalArgumentException("계좌를 찾을 수 없습니다"));
                
                DistributedAccount toAccount = accountRepository
                    .findByAccountNumber(toAccountNumber)
                    .orElseThrow(() -> new IllegalArgumentException("계좌를 찾을 수 없습니다"));
                
                // 비즈니스 로직
                fromAccount.withdraw(amount);
                toAccount.deposit(amount);
                
                accountRepository.save(fromAccount);
                accountRepository.save(toAccount);
                
                log.info("분산락 이체 완료: {} → {}", fromAccountNumber, toAccountNumber);
                
            } finally {
                // 락 해제
                if (lock2.isHeldByCurrentThread()) {
                    lock2.unlock();
                }
                if (lock1.isHeldByCurrentThread()) {
                    lock1.unlock();
                }
            }
            
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            throw new RuntimeException("락 획득 중 인터럽트", e);
        }
    }
}
```

## 4.4 Redis 분산락 메커니즘

### Redisson의 Watch Dog 메커니즘

```
[타임라인]

T0   락 획득 (waitTime=10s, leaseTime=3s)
     Redis에 저장: key="account-lock:ACC-001", value=<threadId>, 
                   expire=3s

T1   비즈니스 로직 처리 중... (2.5초 경과)

T2   [Watch Dog 동작]
     잔여 시간 < 1.5초 감지
     → 자동으로 leaseTime 연장
     expire=3s 갱신

T3   비즈니스 로직 계속... (2.5초 경과)

T4   [Watch Dog 동작]
     → 자동으로 leaseTime 연장

T5   작업 완료 → unlock()
     Redis에서 key 삭제
```

### Watch Dog 설정

```yaml
# application.yml
spring:
  redis:
    host: localhost
    port: 6379
```

```java
// Redisson 기본 설정
// lockWatchdogTimeout = 30초 (기본값)
// 이 시간 내에 작업이 완료되지 않으면 자동 연장
```

## 4.5 다양한 분산락 구현

### 1. 세마포어(Semaphore)

```java
/**
 * 제한된 자원 접근 제어
 * - N개의 동시 접근만 허용
 */
@Service
public class RateLimitService {
    
    @Autowired
    private RedissonClient redissonClient;
    
    public void limitedOperation() {
        RSemaphore semaphore = redissonClient.getSemaphore("rate-limit");
        semaphore.setPermits(5); // 5개 동시 요청만 허용
        
        try {
            if (semaphore.tryAcquire()) {
                // 작업 수행
                log.info("작업 수행 중...");
            } else {
                log.warn("할당량 초과");
            }
        } finally {
            semaphore.release();
        }
    }
}
```

### 2. ReadWrite Lock

```java
/**
 * 읽기/쓰기 락
 * - 여러 읽기는 동시 허용
 * - 쓰기는 배타적 접근만 허용
 */
@Service
public class CacheService {
    
    @Autowired
    private RedissonClient redissonClient;
    
    public Object readData(String key) {
        RReadWriteLock lock = redissonClient.getReadWriteLock(key);
        lock.readLock().lock();
        try {
            return retrieveFromDB(key);
        } finally {
            lock.readLock().unlock();
        }
    }
    
    public void writeData(String key, Object value) {
        RReadWriteLock lock = redissonClient.getReadWriteLock(key);
        lock.writeLock().lock();
        try {
            saveToDB(key, value);
        } finally {
            lock.writeLock().unlock();
        }
    }
}
```

### 3. Fair Lock (공정한 락)

```java
/**
 * 락 획득 순서를 보장하는 공정한 락
 * - FIFO 순서로 락 획득
 * - 기아(Starvation) 방지
 */
@Service
public class FairLockService {
    
    @Autowired
    private RedissonClient redissonClient;
    
    public void fairOperation() {
        RLock fairLock = redissonClient.getFairLock("fair-lock");
        
        try {
            if (fairLock.tryLock(10, 3, TimeUnit.SECONDS)) {
                // 비즈니스 로직
                log.info("공정한 락으로 보호된 작업 수행");
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        } finally {
            if (fairLock.isHeldByCurrentThread()) {
                fairLock.unlock();
            }
        }
    }
}
```

## 4.6 특징

| 항목 | 설명 |
|------|-----|
| **장점** | • 분산 환경 지원<br>• 다중 인스턴스 간 동시성 제어<br>• 유연한 타임아웃 설정<br>• 여러 락 타입 제공 |
| **단점** | • Redis 별도 인프라 필요<br>• 네트워크 지연 고려<br>• Watch Dog 메커니즘 이해 필요 |
| **사용 시기** | • 마이크로서비스 아키텍처<br>• 다중 인스턴스 배포<br>• 높은 동시성 + 안정성 |

---

# 5. 비교 분석

## 5.1 종합 비교표

| 특성 | 낙관락 | 비관락 | 분산락 |
|------|--------|--------|--------|
| **환경** | 단일 DB | 단일 DB | 다중 인스턴스 |
| **메커니즘** | 버전 필드 | 행 잠금 | Redis 락 |
| **동시성** | 매우 높음 | 중간 | 중간~높음 |
| **응답 속도** | 빠름 | 느림(대기) | 중간 |
| **충돌 빈도** | 낮음 | 높음 | 보통 |
| **재시도** | 필요 | 불필요 | 불필요 |
| **데드락** | 없음 | 가능 | 없음 |
| **구현 복잡도** | 낮음 | 낮음 | 높음 |
| **인프라** | DB만 | DB만 | DB + Redis |

## 5.2 선택 가이드

```
┌─ 충돌 빈도가 낮은가?
│  ├─ Yes → 낙관락 선택
│  └─ No  → 다음 항목 확인
│
└─ 분산 환경인가?
   ├─ Yes → 분산락 선택 (Redis/Zookeeper)
   └─ No  → 비관락 선택
```

### 예시 시나리오

```
1. 온라인 쇼핑몰 상품 정보 수정
   → 낙관락 (조회 많음, 수정 드묾)

2. 은행 계좌 이체
   → 비관락 또는 분산락 (높은 정확성 필요, 충돌 예상)

3. 분산 시스템의 마이크로서비스 간 상태 관리
   → 분산락 (여러 인스턴스, 높은 동시성)

4. 게임 서버의 인벤토리 관리
   → 분산락 + 비관락 (다중 인스턴스, 높은 동시성)
```

---

# 6. 실제 샘플 프로젝트

## 6.1 프로젝트 구조

전체 샘플 코드는 아래 저장소에서 확인 가능합니다.

```
distributed-lock-samples/
├── pom.xml
├── src/main/
│   ├── java/com/gracefulsoul/lock/
│   │   ├── DistributedLockSamplesApplication.java
│   │   ├── DataInitializer.java
│   │   ├── config/
│   │   │   └── RedissonConfig.java
│   │   ├── domain/
│   │   │   ├── OptimisticAccount.java
│   │   │   ├── PessimisticAccount.java
│   │   │   └── DistributedAccount.java
│   │   ├── repository/
│   │   │   ├── OptimisticAccountRepository.java
│   │   │   ├── PessimisticAccountRepository.java
│   │   │   └── DistributedAccountRepository.java
│   │   ├── service/
│   │   │   ├── OptimisticLockService.java
│   │   │   ├── PessimisticLockService.java
│   │   │   └── DistributedLockService.java
│   │   └── controller/
│   │       └── AccountController.java
│   └── resources/
│       └── application.yml
└── src/test/
    └── java/com/gracefulsoul/lock/service/
        ├── OptimisticLockServiceTest.java
        └── PessimisticLockServiceTest.java
```

## 6.2 주요 의존성

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>

<dependency>
    <groupId>org.redisson</groupId>
    <artifactId>redisson-spring-boot-starter</artifactId>
    <version>3.24.3</version>
</dependency>

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

## 6.3 API 사용 예제

### 낙관락 API
```bash
# 이체
curl "http://localhost:8080/api/accounts/optimistic/transfer?from=OPT-001&to=OPT-002&amount=1000"

# 입금
curl -X POST "http://localhost:8080/api/accounts/optimistic/deposit?accountNumber=OPT-001&amount=5000"

# 출금
curl -X POST "http://localhost:8080/api/accounts/optimistic/withdraw?accountNumber=OPT-001&amount=2000"
```

### 비관락 API
```bash
# 이체
curl -X POST "http://localhost:8080/api/accounts/pessimistic/transfer?from=PES-001&to=PES-002&amount=1000"

# 잔액 조회
curl "http://localhost:8080/api/accounts/pessimistic/balance?accountNumber=PES-001"
```

### 분산락 API
```bash
# 이체
curl -X POST "http://localhost:8080/api/accounts/distributed/transfer?from=DIS-001&to=DIS-002&amount=1000"

# 입금
curl -X POST "http://localhost:8080/api/accounts/distributed/deposit?accountNumber=DIS-001&amount=3000"
```

---

# 7. 성능 고려사항

## 7.1 벤치마크 시나리오

| 시나리오 | 낙관락 | 비관락 | 분산락 |
|--------|--------|--------|--------|
| **낮은 충돌 (1% 이하)** | 🟢 매우 우수 | 🟡 보통 | 🟡 보통 |
| **중간 충돌 (5~10%)** | 🟡 보통 | 🟢 우수 | 🟡 보통 |
| **높은 충돌 (20% 이상)** | 🔴 나쁨 | 🟢 우수 | 🟢 우수 |
| **높은 동시성** | 🟢 우수 | 🟡 보통 | 🟡 보통 |
| **다중 인스턴스** | 🔴 불가능 | 🔴 불가능 | 🟢 우수 |

## 7.2 최적화 팁

### 낙관락 최적화
```java
// 1. 배치 처리로 재시도 횟수 줄이기
@Transactional
public void batchTransfer(List<TransferRequest> requests) {
    for (TransferRequest req : requests) {
        // 각각 재시도 가능
        transfer(req.from, req.to, req.amount);
    }
}

// 2. 버전 필드의 데이터타입 최적화
@Version
private Short version; // Long 대신 Short 사용 (작은 범위)
```

### 비관락 최적화
```java
// 1. 타임아웃 설정
@PessimisticLock
@QueryTimeout(value = 5, timeUnit = TimeUnit.SECONDS)
Optional<PessimisticAccount> findWithTimeout(String id);

// 2. 배치 업데이트
@Modifying
@Query("UPDATE PessimisticAccount SET balance = balance - :amount WHERE id IN :ids")
int updateBatch(@Param("ids") List<Long> ids, @Param("amount") Long amount);
```

### 분산락 최적화
```java
// 1. Watch Dog 타임아웃 조정
Config config = new Config();
config.setLockWatchdogTimeout(20000); // 20초 (기본: 30초)

// 2. 락 타입별 최적화
RLock lock = redissonClient.getFairLock(key); // 공정성 필요 시
```

---

# 8. 주요 제품 및 기술

## 8.1 분산락 솔루션

| 제품 | 특징 | 용도 |
|------|------|------|
| **Redis + Redisson** | 재진입 가능, Watch Dog, 다양한 락 타입 | 일반적인 분산락 |
| **Apache Zookeeper** | 높은 안정성, 강한 일관성 | 복잡한 분산 조정 |
| **Consul** | 서비스 디스커버리 통합, 세션 기반 락 | 마이크로서비스 |
| **etcd** | Kubernetes 친화적, ACID 트랜잭션 | K8s 환경 |

## 8.2 데이터베이스별 비관락 지원

| DB | PESSIMISTIC_READ | PESSIMISTIC_WRITE | 타임아웃 |
|----|--------------------|-------------------|--------|
| **MySQL (InnoDB)** | SELECT ... FOR UPDATE SHARED | SELECT ... FOR UPDATE | NOWAIT / SKIP LOCKED |
| **PostgreSQL** | SELECT ... FOR UPDATE SHARED | SELECT ... FOR UPDATE | NOWAIT / SKIP LOCKED |
| **Oracle** | SELECT ... FOR UPDATE | SELECT ... FOR UPDATE | 타임아웃 설정 가능 |
| **SQL Server** | WITH(NOLOCK) | WITH(XLOCK) | 타임아웃 설정 가능 |

---

# 9. 개념 정리

## 9.1 핵심 용어

| 용어 | 설명 |
|------|------|
| **트랜잭션(Transaction)** | 여러 DB 작업의 원자적 실행 단위 |
| **격리 수준(Isolation Level)** | 동시 트랜잭션 간 데이터 보호 수준 (DIRTY_READ, REPEATABLE_READ 등) |
| **데드락(Deadlock)** | 두 개 이상의 트랜잭션이 서로 대기하는 상태 |
| **락(Lock)** | 다른 트랜잭션의 접근을 제한하는 메커니즘 |
| **배타락(Exclusive Lock)** | 읽기/쓰기 모두 차단하는 락 |
| **공유락(Shared Lock)** | 읽기만 허용하고 쓰기는 차단하는 락 |
| **Watch Dog** | 자동으로 락 시간을 연장하는 메커니즘 |

## 9.2 ACID 특성과의 관계

```
A - Atomicity (원자성)
    모두 성공 또는 모두 실패
    → 낙관락, 비관락, 분산락 모두 보장

C - Consistency (일관성)
    데이터 규칙 준수
    → 비관락과 분산락이 강함

I - Isolation (격리성)
    트랜잭션 간 독립성
    → 낙관락은 약함, 비관락은 강함

D - Durability (내구성)
    커밋 후 데이터 지속
    → DB가 담당
```

---

# 참조

## 공식 문서

- [Spring Data JPA - Locking](https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods/query-method-details.html#jpa.locking){:target="_blank"}
- [Hibernate - Optimistic and Pessimistic Locking](https://docs.jboss.org/hibernate/orm/6.0/userguide/html_single/Hibernate_User_Guide.html#pc-custom-locking){:target="_blank"}
- [Redisson - Distributed Locks](https://redisson.org/features/distributed-locks-and-synchronizers.html){:target="_blank"}

## 기술 블로그

- [Baeldung - A Guide to Locks in Spring Data JPA](https://www.baeldung.com/jpa-pessimistic-locking){:target="_blank"}
- [Redisson - Lock Mechanisms](https://redisson.org/features/distributed-locks-and-synchronizers.html){:target="_blank"}
- [DZone - Distributed Locking in Microservices](https://dzone.com/articles/distributed-locking-in-microservices){:target="_blank"}

## 샘플 코드 저장소

- [GracefulSoul/distributed-lock-samples](https://github.com/GracefulSoul/distributed-lock-samples){:target="_blank"}

## 참고 자료

- MySQL 공식 문서: [SELECT ... FOR UPDATE](https://dev.mysql.com/doc/refman/8.0/en/commit.html){:target="_blank"}
- PostgreSQL 공식 문서: [Explicit Locking](https://www.postgresql.org/docs/current/explicit-locking.html){:target="_blank"}
- Redis 공식 문서: [Redis as a Lock Manager](https://redis.io/docs/manual/client-side-caching/){:target="_blank"}

---

# 결론

데이터 동시성 제어는 안정적인 애플리케이션 운영의 핵심입니다. 
각 락 메커니즘의 특성을 이해하고 상황에 맞게 선택하는 것이 중요합니다:

- **낙관락**: 충돌이 드문 조회 위주의 작업
- **비관락**: 충돌이 빈번한 수정 작업
- **분산락**: 다중 인스턴스 환경에서의 안전한 동시성 제어

본 글의 샘플 코드를 참고하여 자신의 프로젝트에 맞는 방식을 구현하길 권장합니다.

**소스 코드**는 [GracefulSoul/distributed-lock-samples](https://github.com/GracefulSoul/distributed-lock-samples){:target="_blank"}에서 확인 가능합니다.
