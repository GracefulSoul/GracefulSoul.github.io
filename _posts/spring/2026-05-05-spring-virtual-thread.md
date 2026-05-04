---
title: "Spring Boot 4.0.5에서 VirtualThread 활용하기"
excerpt: "Java 25 + Spring Boot 4.0.5 환경에서 Project Loom의 VirtualThread를 활용하는 방법을 소개합니다. VirtualThread의 개념, 메커니즘, Thread Pinning 문제 및 해결책을 실제 코드 예제와 함께 설명합니다."
last_modified_at: 2026-05-05T10:00:00
header:
  image: /assets/images/spring/virtual-thread-spring.png
categories:
  - Spring
tags:
  - Programming
  - Spring
  - VirtualThread
  - Java25
  - ProjectLoom
  - Concurrency

toc: true
toc_ads: true
toc_sticky: true
---

# VirtualThread 개요

VirtualThread(가상 스레드)는 Java 21에서 Preview로 도입되고 Java 25에서 정식으로 포함된 경량 스레드 기능입니다. [Project Loom](https://openjdk.org/projects/loom/){:target="_blank"} 프로젝트의 핵심 성과물로, 동시 실행 애플리케이션의 개발을 단순화하고 성능을 향상시킵니다.

## VirtualThread의 개념

VirtualThread는 **논리적 스레드(Logical Thread)**로, OS 수준의 Platform Thread(물리적 스레드)에 직접 매핑되지 않습니다. 대신 JVM이 관리하는 **Carrier Thread**(Platform Thread 풀)에서 실행되며, 효율적으로 스케줄링됩니다.

### 핵심 특징

1. **경량성**: Platform Thread는 약 2MB의 메모리를 사용하지만, VirtualThread는 약 1KB만 사용합니다.
2. **대규모 동시성**: 수백만 개의 VirtualThread를 생성할 수 있습니다.
3. **자동 스케줄링**: JVM이 Carrier Thread에 VirtualThread를 효율적으로 할당합니다.
4. **I/O 최적화**: I/O 대기 중에는 Carrier Thread가 다른 VirtualThread를 처리할 수 있습니다.

---

# VirtualThread 메커니즘

## 내부 동작 원리

### 1. Structured Concurrency

VirtualThread는 **구조화된 동시성(Structured Concurrency)**을 통해 작업의 생명주기를 명확하게 관리합니다.

```java
// VirtualThread 풀 생성 및 작업 실행
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    for (int i = 0; i < 1000; i++) {
        int taskId = i;
        executor.submit(() -> {
            // 작업 수행
            processTask(taskId);
        });
    }
    // try-with-resources 블록을 벗어날 때까지 모든 작업 완료 대기
}
```

### 2. Carrier Thread와 Virtual Thread의 관계

```
┌─────────────────────────────────────────────────────┐
│              JVM Virtual Threads Scheduler           │
├─────────────────────────────────────────────────────┤
│  VThread 1   │  VThread 2   │  ...  │  VThread N   │
└────┬──────────────┬──────────────────┬──────────────┘
     │              │                  │
  ┌──▼──┐        ┌──▼──┐           ┌──▼──┐
  │Carr │        │Carr │           │Carr │
  │ Thread 1     │ Thread 2  ...   │ Thread M
  └──────┘        └──────┘           └──────┘
     (Platform Threads - OS Level)
```

### 3. Virtual Thread의 상태 전환

```
┌──────────────┐
│   NEW        │ 생성됨
└──────┬───────┘
       │
┌──────▼───────┐
│  RUNNABLE    │ 실행 가능
└──────┬───────┘
       │ (Carrier Thread에 할당)
┌──────▼───────┐
│  RUNNING     │ 실행 중
└──────┬───────┘
       │ (I/O 대기 또는 yield)
┌──────▼───────┐
│  WAITING     │ 대기 중
└──────┬───────┘
       │ (Carrier Thread에서 해제)
┌──────▼───────┐
│  TERMINATED  │ 완료
└──────────────┘
```

---

# VirtualThread와 Platform Thread의 차이점

## 성능 비교

| 특성 | Platform Thread | VirtualThread |
|------|-----------------|---------------|
| **메모리 사용** | ~2MB | ~1KB |
| **생성 시간** | ~1ms | ~0.01ms |
| **생성 가능 개수** | 수천~수만 개 | 수백만 개 |
| **컨텍스트 스위칭** | OS 스케줄러 관리 | JVM 스케줄러 관리 |
| **I/O 블로킹** | OS 수준에서 블로킹 | JVM 수준에서 처리 |
| **Thread Pinning** | 없음 | synchronized 사용 시 발생 |

## 실제 메모리 사용량 측정

```java
public void compareMemoryUsage(int count) {
    // Platform Thread 메모리 측정
    long platformBefore = Runtime.getRuntime().totalMemory() 
                        - Runtime.getRuntime().freeMemory();
    try (ExecutorService platformExecutor = Executors.newFixedThreadPool(count)) {
        IntStream.range(0, count).forEach(i -> {
            platformExecutor.submit(() -> {
                try { Thread.sleep(2000); } catch (InterruptedException e) {}
            });
        });
    }
    long platformAfter = Runtime.getRuntime().totalMemory() 
                       - Runtime.getRuntime().freeMemory();
    
    // Virtual Thread 메모리 측정
    long virtualBefore = Runtime.getRuntime().totalMemory() 
                       - Runtime.getRuntime().freeMemory();
    try (ExecutorService virtualExecutor = Executors.newVirtualThreadPerTaskExecutor()) {
        IntStream.range(0, count).forEach(i -> {
            virtualExecutor.submit(() -> {
                try { Thread.sleep(2000); } catch (InterruptedException e) {}
            });
        });
    }
    long virtualAfter = Runtime.getRuntime().totalMemory() 
                      - Runtime.getRuntime().freeMemory();
    
    long platformMemory = Math.abs(platformAfter - platformBefore);
    long virtualMemory = Math.abs(virtualAfter - virtualBefore);
    
    System.out.println("Platform Thread Memory: " + platformMemory + " bytes");
    System.out.println("Virtual Thread Memory: " + virtualMemory + " bytes");
    System.out.println("Memory Savings: " + (platformMemory - virtualMemory) + " bytes");
}
```

---

# VirtualThread의 내부 구조

## Thread 클래스의 확장

Java 25에서 VirtualThread는 Thread 클래스와 호환되도록 설계되었습니다.

```java
// VirtualThread 식별
Thread current = Thread.currentThread();
boolean isVirtual = current.isVirtual();
long threadId = current.threadId();
String threadName = current.getName();

System.out.println("IsVirtual: " + isVirtual);       // true
System.out.println("ThreadID: " + threadId);          // 고유한 ID
System.out.println("ThreadName: " + threadName);      // virtual-thread-0
```

## Carrier Thread 접근

Java 25에서는 VirtualThread가 현재 할당된 Carrier Thread에 접근할 수 있습니다.

```java
// VirtualThread 생성 및 Carrier Thread 정보 출력
Thread vthread = Thread.ofVirtual().start(() -> {
    System.out.println("VirtualThread running on: " 
        + Thread.currentThread().getName());
    
    // 현재 스택 정보
    StackTraceElement[] stackTrace = Thread.currentThread().getStackTrace();
    for (StackTraceElement element : stackTrace) {
        System.out.println("  at " + element);
    }
});

vthread.join();
```

---

# VirtualThread 사용 방법

## 1. Spring Boot에서 @Async 사용

```java
@Service
@Slf4j
public class VirtualThreadBasicService {
    
    @Bean(name = "virtualThreadExecutor")
    public Executor virtualThreadExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setCorePoolSize(10);
        executor.setMaxPoolSize(100);
        executor.setQueueCapacity(500);
        executor.setThreadNamePrefix("virtual-thread-");
        executor.initialize();
        return executor;
    }
    
    @Async("virtualThreadExecutor")
    public CompletableFuture<String> processWithVirtualThread(int taskId) {
        try {
            log.info("Task {} - VirtualThread: {}", 
                taskId, 
                Thread.currentThread().isVirtual());
            
            Thread.sleep(1000); // I/O 모의
            return CompletableFuture.completedFuture("Completed");
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            return CompletableFuture.failedFuture(e);
        }
    }
}
```

## 2. ExecutorService를 통한 직접 생성

```java
// 각 작업마다 새로운 VirtualThread 생성
public void demonstrateDirectVirtualThreadCreation() {
    try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
        for (int i = 0; i < 10; i++) {
            int taskId = i;
            executor.submit(() -> {
                System.out.println("Task " + taskId + 
                    " running on " + Thread.currentThread().getName());
                try { Thread.sleep(500); } catch (InterruptedException e) {}
            });
        }
    }
}
```

## 3. 맞춤형 VirtualThread Factory

```java
// 이름과 우선순위를 지정하여 VirtualThread 생성
ThreadFactory virtualThreadFactory = Thread.ofVirtual()
    .name("custom-vthread-", 0)
    .uncaughtExceptionHandler((t, e) -> {
        System.err.println("Exception in " + t.getName() + ": " + e.getMessage());
    })
    .factory();

try (ExecutorService executor = Executors.newThreadPerTaskExecutor(virtualThreadFactory)) {
    for (int i = 0; i < 1000; i++) {
        executor.submit(() -> {
            // 작업 수행
        });
    }
}
```

---

# Thread Pinning 문제

## Java 21의 Thread Pinning 이슈

Java 21에서 VirtualThread는 synchronized 키워드 사용 시 **Thread Pinning** 문제가 발생했습니다.

### Thread Pinning이란?

VirtualThread가 Carrier Thread에서 **벗어나지 못하고 고정되는 현상**입니다. 이로 인해 다른 VirtualThread가 해당 Carrier Thread를 사용할 수 없게 됩니다.

```java
// Java 21에서 Thread Pinning 발생
public synchronized void criticalSection() {
    // VirtualThread가 여기에서 Carrier Thread에 고정됨
    // Carrier Thread를 놓지 못함
    Thread.sleep(1000);
}
```

### Thread Pinning 발생 원인

1. **synchronized 키워드**: Monitor 기반 동기화
2. **native 메서드 호출**: JNI를 통한 네이티브 코드 실행
3. **외부 라이브러리**: 동기화된 외부 API 사용

### 성능 영향

```
정상 상황:
┌──────────────────┐
│  VirtualThread 1 │ ──┐
├──────────────────┤  │
│  VirtualThread 2 │ ──┤─▶ Carrier Thread (번갈아가며 실행)
├──────────────────┤  │
│  VirtualThread 3 │ ──┘
└──────────────────┘

Thread Pinning 발생:
┌──────────────────────────┐
│  VirtualThread 1 (Pinned)│ ──▶ Carrier Thread (고정됨 - 낭비)
├──────────────────────────┤
│  VirtualThread 2         │ ──▶ 다른 Carrier Thread 필요
├──────────────────────────┤
│  VirtualThread 3         │ ──▶ 다른 Carrier Thread 필요
└──────────────────────────┘
```

---

# Java 24의 Thread Pinning 개선

## synchronized 자동 최적화

Java 24부터는 synchronized 키워드가 자동으로 최적화되어 많은 경우 Thread Pinning 없이 동작합니다.

### 최적화 메커니즘

1. **Monitor 최적화**: 경량 모니터를 사용하여 불필요한 pinning 제거
2. **바이어스 락킹**: 단일 스레드 접근 최적화
3. **잠금 제거**: 접근 분석을 통한 불필요한 잠금 제거

### Java 24 vs Java 21 코드 비교

```java
// Java 21: Thread Pinning 발생
public synchronized void processJava21() {
    // ❌ Carrier Thread에 고정됨
    for (int i = 0; i < 1000; i++) {
        try { Thread.sleep(10); } catch (InterruptedException e) {}
    }
}

// Java 24: 자동 최적화로 Thread Pinning 없음
public synchronized void processJava24() {
    // ✓ 대부분의 경우 Carrier Thread에 고정되지 않음
    for (int i = 0; i < 1000; i++) {
        try { Thread.sleep(10); } catch (InterruptedException e) {}
    }
}
```

### 측정 가능한 개선

```java
public void compareLockPerformance(int taskCount) {
    // synchronized 성능 테스트
    long syncStart = System.nanoTime();
    try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
        IntStream.range(0, taskCount).forEach(i -> {
            executor.submit(() -> synchronizedBlock(i));
        });
    }
    long syncTime = (System.nanoTime() - syncStart) / 1_000_000;
    
    // ReentrantLock 성능 테스트
    long lockStart = System.nanoTime();
    try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
        IntStream.range(0, taskCount).forEach(i -> {
            executor.submit(() -> reentrantLockMethod(i));
        });
    }
    long lockTime = (System.nanoTime() - lockStart) / 1_000_000;
    
    System.out.println("Synchronized: " + syncTime + "ms");
    System.out.println("ReentrantLock: " + lockTime + "ms");
}
```

---

# ReentrantLock을 사용한 Thread Pinning 해결

## ReentrantLock의 우수성

Java 21에서는 synchronized 대신 **ReentrantLock**을 사용하여 Thread Pinning을 회피합니다.

### 코드 예제

```java
private final ReentrantLock lock = new ReentrantLock();

// synchronized 대신 ReentrantLock 사용
public void criticalSection(int taskId) {
    lock.lock();
    try {
        // Thread Pinning 없음
        System.out.println("Task " + taskId + 
            " running on " + Thread.currentThread().getName());
        Thread.sleep(100);
    } catch (InterruptedException e) {
        Thread.currentThread().interrupt();
    } finally {
        lock.unlock();
    }
}
```

### synchronized vs ReentrantLock 성능 비교

| 동기화 방식 | Java 21 | Java 24+ | 권장사항 |
|-----------|---------|---------|---------|
| **synchronized** | ❌ Thread Pinning | ✓ 자동 최적화 | 간단한 경우만 |
| **ReentrantLock** | ✓ Pinning 없음 | ✓ Pinning 없음 | 모든 경우 권장 |
| **StampedLock** | ✓ Pinning 없음 | ✓ Pinning 없음 | 읽기 많은 경우 |

---

# Spring Boot 4.0.5에서의 VirtualThread 지원

## 자동 설정

Spring Boot 4.0.5부터는 VirtualThread를 기본적으로 지원합니다.

### application.yml 설정

```yaml
spring:
  application:
    name: spring-virtual-thread-sample
  threads:
    virtual:
      enabled: true

server:
  port: 8080
  tomcat:
    threads:
      max: 200
      min-spare: 10

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  endpoint:
    health:
      show-details: always
```

## RestController에서의 사용

```java
@RestController
@RequestMapping("/api/virtual-thread")
@RequiredArgsConstructor
public class VirtualThreadController {
    
    private final VirtualThreadBasicService basicService;
    
    @GetMapping("/async/{taskId}")
    public CompletableFuture<String> asyncProcess(@PathVariable int taskId) {
        return basicService.processWithVirtualThread(taskId);
    }
    
    @GetMapping("/memory-comparison/{count}")
    public String compareMemory(@PathVariable int count) {
        basicService.compareMemoryUsage(count);
        return "Memory comparison completed";
    }
}
```

---

# VirtualThread의 장점

## 1. 확장성 향상

```java
// Platform Thread: 수천 개의 동시 연결만 가능
// VirtualThread: 수백만 개의 동시 연결 가능
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    for (int i = 0; i < 1_000_000; i++) {
        executor.submit(this::handleRequest);
    }
}
```

## 2. 간단한 코드 작성

```java
// 기존: 복잡한 비동기 처리
CompletableFuture.supplyAsync(() -> {
    return fetchData();
})
.thenApply(data -> processData(data))
.thenAccept(result -> sendResponse(result));

// VirtualThread: 동기 코드처럼 작성
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> {
        var data = fetchData();
        var result = processData(data);
        sendResponse(result);
    });
}
```

## 3. 리소스 효율성

```java
// 비용이 거의 없음
for (int i = 0; i < 10_000; i++) {
    Thread.ofVirtual().start(() -> {
        // 각 작업이 별도의 스택 공간만 필요
    });
}
```

## 4. 예측 가능한 성능

```java
// 일관된 응답 시간
public CompletableFuture<String> consistentPerformance() {
    return CompletableFuture.supplyAsync(() -> {
        // VirtualThread는 I/O 대기를 효율적으로 처리
        var data = callExternalService();
        return processData(data);
    });
}
```

---

# VirtualThread의 단점

## 1. 메모리 오버헤드 (누적 시)

```java
// 매우 많은 VirtualThread를 생성할 때
// 각 스택이 누적되면 메모리 사용량 증가 가능
for (int i = 0; i < 10_000_000; i++) {
    Thread.ofVirtual().start(() -> {
        // 충분한 메모리 필요
    });
}
```

## 2. 플랫폼 종속성

```java
// Java 21 이전 버전에서는 사용 불가
// 점진적 마이그레이션 필요
if (Runtime.version().feature() >= 21) {
    // VirtualThread 사용 가능
}
```

## 3. 디버깅 어려움

```java
// 많은 VirtualThread 동시 실행 시 디버깅 복잡
// 스택 트레이스 분석 어려움
Thread.ofVirtual().start(() -> {
    // 문제 추적 어려움
    performComplexOperation();
});
```

## 4. 라이브러리 호환성

```java
// 일부 라이브러리가 VirtualThread를 지원하지 않을 수 있음
try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
    executor.submit(() -> {
        // 일부 JNI 라이브러리는 Thread Pinning 발생
        nativeLibraryCall();
    });
}
```

---

# 실제 활용 샘플

## 웹 서버 요청 처리

```java
@RestController
@RequestMapping("/api")
@RequiredArgsConstructor
public class RequestHandler {
    
    private final UserService userService;
    private final DataService dataService;
    
    @GetMapping("/user/{id}")
    public CompletableFuture<User> getUser(@PathVariable Long id) {
        return CompletableFuture.supplyAsync(() -> {
            // VirtualThread에서 실행됨
            return userService.getUserById(id);
        });
    }
    
    @PostMapping("/batch-process")
    public CompletableFuture<String> batchProcess(@RequestBody List<Item> items) {
        return CompletableFuture.supplyAsync(() -> {
            // 각 아이템을 병렬로 처리
            items.parallelStream()
                 .forEach(item -> dataService.process(item));
            return "Batch processing completed";
        });
    }
}
```

## I/O 집약적 작업

```java
@Service
@Slf4j
public class FileProcessingService {
    
    private final ExecutorService executor = 
        Executors.newVirtualThreadPerTaskExecutor();
    
    public void processMultipleFiles(List<String> fileNames) {
        for (String fileName : fileNames) {
            executor.submit(() -> {
                try {
                    // 각 파일을 별도의 VirtualThread에서 처리
                    String content = Files.readString(Paths.get(fileName));
                    processContent(content);
                    log.info("Processed: {}", fileName);
                } catch (IOException e) {
                    log.error("Error processing file: {}", fileName, e);
                }
            });
        }
    }
    
    private void processContent(String content) {
        // 시간이 걸리는 처리
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
    }
}
```

## 데이터베이스 쿼리 병렬 처리

```java
@Service
@Slf4j
public class DatabaseService {
    
    @Autowired
    private JdbcTemplate jdbcTemplate;
    
    public List<User> searchMultipleConditions(SearchCriteria criteria) {
        try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
            
            List<CompletableFuture<List<User>>> futures = new ArrayList<>();
            
            // 여러 조건으로 동시에 쿼리 실행
            futures.add(CompletableFuture.supplyAsync(() ->
                searchByDepartment(criteria.getDepartment()), executor
            ));
            futures.add(CompletableFuture.supplyAsync(() ->
                searchByLocation(criteria.getLocation()), executor
            ));
            futures.add(CompletableFuture.supplyAsync(() ->
                searchByRole(criteria.getRole()), executor
            ));
            
            // 모든 결과를 수집
            return futures.stream()
                .map(CompletableFuture::join)
                .flatMap(List::stream)
                .distinct()
                .collect(Collectors.toList());
        }
    }
    
    private List<User> searchByDepartment(String dept) {
        return jdbcTemplate.query(
            "SELECT * FROM users WHERE department = ?",
            new Object[]{dept},
            new UserRowMapper()
        );
    }
    
    private List<User> searchByLocation(String location) {
        // 비슷한 구현
        return new ArrayList<>();
    }
    
    private List<User> searchByRole(String role) {
        // 비슷한 구현
        return new ArrayList<>();
    }
}
```

---

# 주요 코드 정리

## VirtualThread 생성 방식 비교

| 방식 | 코드 | 용도 |
|-----|------|------|
| **@Async** | `@Async("executor")` | Spring Bean에서 비동기 처리 |
| **newVirtualThreadPerTaskExecutor** | `Executors.newVirtualThreadPerTaskExecutor()` | 작업당 스레드 생성 |
| **Thread.ofVirtual** | `Thread.ofVirtual().start(...)` | 단일 VirtualThread 생성 |
| **ofVirtual().factory** | `Thread.ofVirtual().factory()` | 맞춤형 ThreadFactory |

## 동기화 방식 선택 가이드

```
상황별 권장 동기화 방식:

Java 21:
  - I/O 작업 ──> ReentrantLock 또는 StampedLock
  - CPU 작업 ──> ReentrantLock

Java 24+:
  - 간단한 동기화 ──> synchronized 또는 ReentrantLock
  - 복잡한 동기화 ──> ReentrantLock
  - 읽기 많음 ──> StampedLock

Java 25:
  - 모든 경우 ──> ReentrantLock 권장 (안정성)
  - 또는 ──> synchronized (대부분의 경우 최적화됨)
```

---

# 마이그레이션 체크리스트

VirtualThread로 마이그레이션할 때 확인사항:

- [ ] Java 버전 확인 (21 이상 필요)
- [ ] Spring Boot 버전 확인 (3.2 이상 권장)
- [ ] synchronized 키워드 사용 검토
- [ ] 외부 라이브러리의 VirtualThread 지원 확인
- [ ] Thread Pinning 가능성 분석
- [ ] 성능 테스트 수행
- [ ] 모니터링 및 메트릭 설정
- [ ] 점진적 마이그레이션 계획 수립

---

# VirtualThread 테스트 코드

Spring Boot 프로젝트에서 VirtualThread를 테스트하는 방법입니다.

## JUnit 5 테스트 작성

```java
@Slf4j
@DisplayName("VirtualThread Service Tests")
public class VirtualThreadServiceTest {

    private final VirtualThreadBasicService basicService = new VirtualThreadBasicService();
    private final ThreadPinningService pinningService = new ThreadPinningService();
    private final IOSimulationService ioService = new IOSimulationService();

    @Test
    @DisplayName("VirtualThread 기본 생성 및 실행")
    public void testVirtualThreadCreation() {
        assertDoesNotThrow(() -> {
            basicService.demonstrateDirectVirtualThreadCreation();
        });
    }

    @Test
    @DisplayName("VirtualThread 풀 생성 및 관리")
    public void testVirtualThreadPool() {
        assertDoesNotThrow(() -> {
            basicService.demonstrateFixedVirtualThreadPool(10);
        });
    }

    @Test
    @DisplayName("VirtualThread 비동기 처리")
    public void testVirtualThreadAsync() {
        CompletableFuture<String> future = basicService.processWithVirtualThread(1);
        
        String result = assertDoesNotThrow(() -> future.get());
        assertTrue(result.contains("completed"));
    }

    @Test
    @DisplayName("Thread Pinning 감지 및 분석")
    public void testThreadPinningDetection() {
        assertDoesNotThrow(() -> {
            pinningService.detectThreadPinning();
        });
    }

    @Test
    @DisplayName("Lock 성능 비교")
    public void testLockPerformance() {
        assertDoesNotThrow(() -> {
            pinningService.compareLockPerformance(100);
        });
    }

    @Test
    @DisplayName("I/O 작업 시뮬레이션")
    public void testIOSimulation() {
        var user = ioService.simulateDatabaseQuery(1L);
        
        assertNotNull(user);
        assertEquals(1L, user.getId());
        assertEquals("User 1", user.getName());
    }

    @Test
    @DisplayName("병렬 I/O 작업")
    public void testParallelIOOperations() {
        List<Long> userIds = Arrays.asList(1L, 2L, 3L, 4L, 5L);
        List<User> users = ioService.fetchMultipleUsers(userIds);
        
        assertEquals(5, users.size());
        assertTrue(users.stream().allMatch(u -> u.getId() != null));
    }

    @Test
    @DisplayName("메모리 사용량 비교")
    public void testMemoryUsageComparison() {
        assertDoesNotThrow(() -> {
            basicService.compareMemoryUsage(100);
        });
    }

    @Test
    @DisplayName("Java 버전 차이점 설명")
    public void testJavaVersionDifferences() {
        String explanation = pinningService.explainJavaVersionDifferences();
        
        assertNotNull(explanation);
        assertTrue(explanation.contains("Java 21"));
        assertTrue(explanation.contains("Java 24"));
        assertTrue(explanation.contains("Java 25"));
    }
}
```

## 테스트 실행

```bash
# 모든 테스트 실행
mvn test

# 특정 테스트 클래스 실행
mvn test -Dtest=VirtualThreadServiceTest

# 특정 테스트 메서드 실행
mvn test -Dtest=VirtualThreadServiceTest#testVirtualThreadAsync

# 테스트 상세 로그 확인
mvn test -X
```

## 테스트 커버리지 측정

```bash
# JaCoCo를 사용한 커버리지 측정
mvn clean test jacoco:report

# 커버리지 리포트 생성
# target/site/jacoco/index.html 확인
```

## 테스트 주요 시나리오

### 1. VirtualThread 생성 테스트
```java
@Test
public void testVirtualThreadCreation() {
    // VirtualThread가 정상적으로 생성되고 실행되는지 확인
    Thread vthread = Thread.ofVirtual().start(() -> {
        assertTrue(Thread.currentThread().isVirtual());
    });
    
    assertDoesNotThrow(vthread::join);
}
```

### 2. 비동기 처리 테스트
```java
@Test
public void testAsyncExecution() {
    CompletableFuture<String> future = basicService.processWithVirtualThread(1);
    
    // 비동기 작업이 완료될 때까지 대기
    String result = assertDoesNotThrow(() -> future.get(5, TimeUnit.SECONDS));
    assertNotNull(result);
}
```

### 3. 동기화 메커니즘 테스트
```java
@Test
public void testSynchronization() {
    // ReentrantLock과 synchronized의 동작 확인
    pinningService.reentrantLockMethod(1);  // ✓ Thread Pinning 없음
    pinningService.synchronizedMethod(1);   // Java 24+에서 최적화됨
}
```

### 4. 성능 비교 테스트
```java
@Test
@DisplayName("Platform Thread vs VirtualThread 성능")
public void performanceBenchmark() {
    long startTime = System.currentTimeMillis();
    
    // VirtualThread 성능 측정
    basicService.demonstrateFixedVirtualThreadPool(1000);
    
    long elapsed = System.currentTimeMillis() - startTime;
    assertTrue(elapsed < 5000, "1000개 VirtualThread 처리 시간이 5초 이내여야 함");
}
```

## 통합 테스트

```java
@SpringBootTest
@DisplayName("VirtualThread 통합 테스트")
public class VirtualThreadIntegrationTest {

    @Autowired
    private VirtualThreadController controller;

    @Test
    public void testAsyncEndpoint() throws Exception {
        // REST API 엔드포인트 테스트
        var result = controller.asyncProcess(1);
        
        assertNotNull(result);
        String response = result.get(5, TimeUnit.SECONDS);
        assertTrue(response.contains("completed"));
    }

    @Test
    public void testVersionDifferencesEndpoint() {
        // Java 버전별 차이점 조회
        String differences = controller.explainVersionDifferences();
        
        assertNotNull(differences);
        assertTrue(differences.contains("Java"));
    }

    @Test
    public void testHealthCheck() {
        String health = controller.health();
        
        assertNotNull(health);
        assertTrue(health.contains("running"));
    }
}
```

## 성능 테스트 (JMH)

대규모 동시 작업의 성능을 측정하는 JMH 벤치마크:

```java
@BenchmarkMode(Mode.Throughput)
@OutputTimeUnit(TimeUnit.SECONDS)
@State(Scope.Benchmark)
public class VirtualThreadBenchmark {

    private final VirtualThreadBasicService service = new VirtualThreadBasicService();

    @Benchmark
    public void benchmarkVirtualThreadCreation() {
        try (ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor()) {
            for (int i = 0; i < 1000; i++) {
                executor.submit(() -> {
                    try { Thread.sleep(10); } catch (InterruptedException e) {}
                });
            }
        }
    }

    @Benchmark
    public void benchmarkPlatformThreadCreation() {
        try (ExecutorService executor = Executors.newFixedThreadPool(10)) {
            for (int i = 0; i < 1000; i++) {
                executor.submit(() -> {
                    try { Thread.sleep(10); } catch (InterruptedException e) {}
                });
            }
        }
    }
}
```

## 테스트 실행 결과 분석

테스트 실행 시 다음 항목을 확인하세요:

1. **VirtualThread 생성**: 밀리초 단위로 빠르게 생성
2. **메모리 사용**: Platform Thread 대비 1/2000 이상 절감
3. **동시성**: 수십만 개 이상의 동시 작업 처리
4. **Thread Pinning**: synchronized 사용 시 감지 가능
5. **성능**: I/O 대기 중 다른 작업 처리 (효율성 향상)

---

# 결론

VirtualThread는 Java 애플리케이션의 동시성 처리를 혁신적으로 개선합니다.

## 핵심 요점

1. **간단함**: 동기 코드처럼 작성 가능
2. **확장성**: 수백만 개의 동시 작업 처리 가능
3. **효율성**: 메모리와 CPU를 효율적으로 사용
4. **호환성**: 기존 Thread API와 호환

## Java 버전별 선택

| Java 버전 | 권장사항 |
|----------|---------|
| 20 이하 | VirtualThread 사용 불가 |
| 21-23 | VirtualThread 사용, ReentrantLock 권장 |
| 24 | VirtualThread 사용, synchronized 일부 가능 |
| 25+ | VirtualThread 사용, synchronized 대부분 가능 |

Spring Boot 4.0.5 환경에서 VirtualThread를 적극 활용하면 높은 성능과 확장성을 갖춘 애플리케이션을 구축할 수 있습니다.

---

# 참고 자료

- [Project Loom - OpenJDK](https://openjdk.org/projects/loom/){:target="_blank"}
- [Virtual Threads - Java 25 Documentation](https://docs.oracle.com/en/java/javase/25/docs/api/java.base/java/lang/VirtualThread.html){:target="_blank"}
- [Java 21 Release Notes](https://openjdk.org/projects/jdk/21/){:target="_blank"}
- [Java 24 Release Notes](https://openjdk.org/projects/jdk/24/){:target="_blank"}
- [Java 25 Release Notes](https://openjdk.org/projects/jdk/25/){:target="_blank"}
- [Spring Framework 4.0 Virtual Thread Support](https://spring.io/){:target="_blank"}
- [Structured Concurrency - JEP 453](https://openjdk.org/jeps/453){:target="_blank"}
- [Thread Pinning and Virtual Threads](https://inside.java/2021/05/10/vthreads/){:target="_blank"}
- [Spring Boot VirtualThread Configuration](https://spring.io/blog){:target="_blank"}
- [GracefulSoul Spring VirtualThread Sample Project](https://github.com/GracefulSoul/spring-virtual-thread-sample){:target="_blank"}

---


현재 프로젝트의 샘플 코드는 [GitHub Repository](https://github.com/GracefulSoul/spring-virtual-thread-sample){:target="_blank"}에서 확인하실 수 있습니다.
