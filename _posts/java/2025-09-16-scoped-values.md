---
title: "Java 25 - Scoped Values (Final)"
excerpt: "Java 25에서 Scoped Values가 최종 기능으로 제공됩니다"
last_modified_at: 2025-09-16T11:00:00
header:
  image: /assets/images/java/java.png
categories:
  - Java
tags:
  - Programming
  - Releases
  - Java 25
  - Scoped Values
  - Threading

toc: true
toc_ads: true
toc_sticky: true
---

# JAVA 25[^Java25]

Scoped Values(범위가 지정된 값)[^ScopedValues]는 Java 25에서 최종 기능으로 제공되는 API입니다. 이 기능은 메서드가 호출하는 다른 메서드들과 같은 스레드 내에서, 그리고 자식 스레드와 불변 데이터를 공유할 수 있도록 합니다. ThreadLocal에 비해 더 효율적이고 안전합니다.

## Scoped Values vs ThreadLocal

ThreadLocal은 오랫동안 사용되었지만 몇 가지 문제가 있습니다:

- **무제한의 가변성**: 언제든지 `set()` 메서드로 값을 변경할 수 있음
- **무한한 생명주기**: `remove()` 호출을 잊으면 메모리 누수 발생
- **높은 상속 비용**: 자식 스레드가 부모 스레드의 모든 ThreadLocal값을 복사해야 함

Scoped Values는 다음을 제공합니다:

- **불변성**: 한 번 설정되면 변경할 수 없음
- **제한된 생명주기**: 스코프를 벗어나면 자동으로 소멸
- **효율적인 상속**: 메모리 복사 없이 자식 스레드와 공유

## 기본 사용 방법

### 1. Scoped Value 선언 및 기본 사용

```java
import java.lang.ScopedValue;
import static java.lang.ScopedValue.where;

public class BasicScopedValueExample {
    
    // Scoped Value 선언
    private static final ScopedValue<String> USERNAME = ScopedValue.newInstance();
    private static final ScopedValue<Integer> USER_ID = ScopedValue.newInstance();
    
    public static void main(String[] args) {
        // 값을 바인딩하여 코드 실행
        where(USERNAME, "Alice")
            .where(USER_ID, 101)
            .run(() -> {
                System.out.println("사용자: " + USERNAME.get());
                System.out.println("ID: " + USER_ID.get());
                performUserOperation();
            });
    }
    
    private static void performUserOperation() {
        System.out.println("사용자 작업 수행 - " + USERNAME.get());
    }
}
```

**실행 결과:**
```
사용자: Alice
ID: 101
사용자 작업 수행 - Alice
```

## 프레임워크 컨텍스트 전달 예제

### 2. 웹 프레임워크에서의 사용

```java
import java.lang.ScopedValue;
import static java.lang.ScopedValue.where;

public class FrameworkContext {
    
    // 프레임워크 컨텍스트
    static class RequestContext {
        private final String requestId;
        private final String userId;
        private final long timestamp;
        
        RequestContext(String requestId, String userId) {
            this.requestId = requestId;
            this.userId = userId;
            this.timestamp = System.currentTimeMillis();
        }
        
        public String getRequestId() { return requestId; }
        public String getUserId() { return userId; }
        public long getTimestamp() { return timestamp; }
    }
    
    // 프레임워크에서 관리하는 Scoped Value
    private static final ScopedValue<RequestContext> CONTEXT = 
        ScopedValue.newInstance();
    
    // 프레임워크의 요청 처리
    public static void handleRequest(String requestId, String userId) {
        RequestContext context = new RequestContext(requestId, userId);
        
        where(CONTEXT, context).run(() -> {
            // 애플리케이션 코드 실행
            Application.processRequest();
            
            // 데이터베이스 쿼리
            Framework.queryDatabase();
        });
    }
    
    // 데이터 접근 계층
    static class Framework {
        public static void queryDatabase() {
            // CONTEXT.get()을 통해 컨텍스트 접근
            RequestContext ctx = CONTEXT.get();
            System.out.println("DB 조회 - 요청ID: " + ctx.getRequestId() 
                             + ", 사용자: " + ctx.getUserId());
        }
    }
    
    // 애플리케이션 코드
    static class Application {
        public static void processRequest() {
            RequestContext ctx = CONTEXT.get();
            System.out.println("요청 처리 - 사용자: " + ctx.getUserId());
        }
    }
    
    public static void main(String[] args) {
        handleRequest("REQ-001", "user123");
    }
}
```

**실행 결과:**
```
요청 처리 - 사용자: user123
DB 조회 - 요청ID: REQ-001, 사용자: user123
```

## 값의 재바인딩

### 3. 중첩된 스코프에서 값 재바인딩

```java
import java.lang.ScopedValue;
import static java.lang.ScopedValue.where;

public class RebindingScopedValue {
    
    private static final ScopedValue<String> CONTEXT = ScopedValue.newInstance();
    
    public static void main(String[] args) {
        where(CONTEXT, "parent").run(() -> {
            System.out.println("부모 스코프: " + CONTEXT.get());
            
            outerMethod();
            
            // 다시 부모 스코프의 값으로 복원됨
            System.out.println("부모 스코프 (복원): " + CONTEXT.get());
        });
    }
    
    private static void outerMethod() {
        // 새로운 값으로 재바인딩
        where(CONTEXT, "child").run(() -> {
            System.out.println("자식 스코프: " + CONTEXT.get());
            innerMethod();
            System.out.println("자식 스코프 (복원): " + CONTEXT.get());
        });
    }
    
    private static void innerMethod() {
        where(CONTEXT, "grandchild").run(() -> {
            System.out.println("손자 스코프: " + CONTEXT.get());
        });
    }
}
```

**실행 결과:**
```
부모 스코프: parent
자식 스코프: child
손자 스코프: grandchild
자식 스코프 (복원): child
부모 스코프 (복원): parent
```

## 가상 스레드[^VirtualThreads]와의 결합

### 4. Structured Concurrency[^StructuredConcurrency]와 통합

```java
import java.lang.ScopedValue;
import java.util.concurrent.StructuredTaskScope;
import static java.lang.ScopedValue.where;

public class ScopedValueWithStructuredConcurrency {
    
    private static final ScopedValue<String> USER_ID = 
        ScopedValue.newInstance();
    
    public static void main(String[] args) throws InterruptedException {
        where(USER_ID, "user-123").run(() -> {
            try (var scope = StructuredTaskScope.open()) {
                
                // 자식 스레드들이 USER_ID 값을 상속받음
                scope.fork(() -> {
                    System.out.println("작업 1 - 사용자: " + USER_ID.get());
                    return "작업 1 완료";
                });
                
                scope.fork(() -> {
                    System.out.println("작업 2 - 사용자: " + USER_ID.get());
                    return "작업 2 완료";
                });
                
                scope.join();
                System.out.println("모든 작업 완료");
                
            } catch (StructuredTaskScope.FailedException e) {
                e.printStackTrace();
            }
        });
    }
}
```

**실행 결과:**
```
작업 1 - 사용자: user-123
작업 2 - 사용자: user-123
모든 작업 완료
```

## 값의 바인딩 여부 확인

### 5. isBound()를 이용한 확인

```java
import java.lang.ScopedValue;
import static java.lang.ScopedValue.where;

public class CheckBindingExample {
    
    private static final ScopedValue<String> SETTING = 
        ScopedValue.newInstance();
    
    public static void main(String[] args) {
        // 바인딩 없이
        checkSetting();
        
        // 바인딩을 통해
        where(SETTING, "enabled").run(() -> {
            checkSetting();
        });
    }
    
    private static void checkSetting() {
        if (SETTING.isBound()) {
            System.out.println("설정값: " + SETTING.get());
        } else {
            System.out.println("설정값이 바인딩되지 않음");
        }
    }
}
```

**실행 결과:**
```
설정값이 바인딩되지 않음
설정값: enabled
```

## 복수 값 바인딩

### 6. 여러 Scoped Value 한 번에 바인딩

```java
import java.lang.ScopedValue;
import static java.lang.ScopedValue.where;

public class MultipleValuesExample {
    
    private static final ScopedValue<String> USERNAME = 
        ScopedValue.newInstance();
    private static final ScopedValue<Integer> ROLE = 
        ScopedValue.newInstance();
    private static final ScopedValue<String> TENANT = 
        ScopedValue.newInstance();
    
    public static void main(String[] args) {
        // 여러 값을 한 번에 바인딩
        where(USERNAME, "Alice")
            .where(ROLE, 5)
            .where(TENANT, "company-x")
            .run(() -> {
                displayUserInfo();
            });
    }
    
    private static void displayUserInfo() {
        System.out.println("사용자명: " + USERNAME.get());
        System.out.println("역할: " + (ROLE.get() == 5 ? "관리자" : "사용자"));
        System.out.println("테넌트: " + TENANT.get());
    }
}
```

**실행 결과:**
```
사용자명: Alice
역할: 관리자
테넌트: company-x
```

## 호출 vs 실행

### 7. call()을 사용한 값 반환

```java
import java.lang.ScopedValue;
import static java.lang.ScopedValue.where;

public class CallReturnValueExample {
    
    private static final ScopedValue<Integer> MULTIPLIER = 
        ScopedValue.newInstance();
    
    public static void main(String[] args) throws Exception {
        int result = where(MULTIPLIER, 10).call(() -> {
            return calculate(5);
        });
        
        System.out.println("결과: " + result);
    }
    
    private static int calculate(int value) {
        return value * MULTIPLIER.get();
    }
}
```

**실행 결과:**
```
결과: 50
```

# 주요 특징 요약

| 특징 | Scoped Values | ThreadLocal |
|------|---------------|------------|
| 불변성 | ✓ (변경 불가) | ✗ (set 호출 가능) |
| 생명주기 | 제한됨 (자동) | 무한 (수동 제거) |
| 메모리 효율 | 높음 | 낮음 |
| 자식 스레드 상속 | 효율적 | 비효율적 |
| API 복잡도 | 간단 | 복잡 |

# 마이그레이션 지침

ThreadLocal에서 Scoped Values로 마이그레이션할 때:

1. **단방향 데이터 전달**인 경우 Scoped Values 추천
2. **양방향 통신**이 필요한 경우 ThreadLocal 유지
3. **메모리 효율**이 중요한 경우 Scoped Values 필수
4. **가상 스레드** 사용 시 Scoped Values 권장

# 주의사항

- `.enable-preview` 플래그 필요:
  ```bash
  javac --enable-preview --release 25 ScopedValueExample.java
  java --enable-preview ScopedValueExample
  ```

- `ScopedValue`는 불변이므로 바인딩 후 변경 불가능
- Structured Concurrency와 함께 사용할 때 가장 효율적

# Reference

[^Java25]: [Oracle-Java_25_Release_Notes](https://docs.oracle.com/en/java/javase/25/docs/api/){:target="_blank"}
[^ScopedValues]: [OpenJDK-JEP 506: Scoped Values](https://openjdk.org/jeps/506){:target="_blank"}
[^VirtualThreads]: [OpenJDK-JEP 444: Virtual Threads](https://openjdk.org/jeps/444){:target="_blank"}
[^StructuredConcurrency]: [OpenJDK-JEP 505: Structured Concurrency](https://openjdk.org/jeps/505){:target="_blank"}
