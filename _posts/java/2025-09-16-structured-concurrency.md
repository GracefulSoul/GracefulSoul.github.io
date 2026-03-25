---
title: "Java 25 - Structured Concurrency (Fifth Preview)"
excerpt: "Java 25에서 구조화된 동시성 API의 최신 기능 소개"
last_modified_at: 2025-09-16T10:00:00
header:
  image: /assets/images/java/java.png
categories:
  - Java
tags:
  - Programming
  - Releases
  - Java 25
  - Concurrency
  - Structured Concurrency

toc: true
toc_ads: true
toc_sticky: true
---

# JAVA 25

구조화된 동시성(Structured Concurrency)은 Java 19부터 도입된 기능으로, 여러 스레드에서 실행되는 관련 작업들을 단일 작업 단위로 취급하여 에러 처리와 취소를 간소화하고, 신뢰성을 높이며, 관찰성(Observability)을 향상시킵니다. Java 25에서는 다섯 번째 프리뷰 버전이 제공됩니다.

## Structured Concurrency의 개념

기존의 `ExecutorService`를 사용한 비구조화된 동시성 프로그래밍은 여러 가지 문제를 야기합니다:

- 하나의 작업이 실패할 때 다른 작업의 취소를 수동으로 처리해야 함
- 스레드 누수(Thread leak) 발생 가능성
- 작업 간의 관계가 코드에 명확하게 드러나지 않음

`StructuredTaskScope`는 이러한 문제들을 해결하여 동시 작업들을 구조적으로 관리할 수 있게 합니다.

## StructuredTaskScope를 이용한 기본 사용 예제

### 병렬 작업 실행 및 결과 처리

```java
import java.util.concurrent.StructuredTaskScope;
import java.util.concurrent.StructuredTaskScope.Subtask;

public class UserOrderResponse {
    record Response(String user, int order) {}
    
    public static Response handle() throws InterruptedException {
        try (var scope = StructuredTaskScope.open()) {
            
            // 두 개의 작업을 병렬로 실행
            Subtask<String> user = scope.fork(() -> findUser());
            Subtask<Integer> order = scope.fork(() -> fetchOrder());
            
            // 모든 작업이 완료될 때까지 대기
            scope.join();
            
            // 결과 조합
            return new Response(user.get(), order.get());
            
        } catch (StructuredTaskScope.FailedException e) {
            System.err.println("작업 실패: " + e.getCause());
            return null;
        }
    }
    
    private static String findUser() {
        return "User123";
    }
    
    private static Integer fetchOrder() {
        return 42;
    }
    
    public static void main(String[] args) throws InterruptedException {
        Response response = handle();
        if (response != null) {
            System.out.println("사용자: " + response.user + ", 주문번호: " + response.order);
        }
    }
}
```

**실행 결과:**
```
사용자: User123, 주문번호: 42
```

## 경쟁 조건 처리 (Race Pattern)

`anySuccessfulResultOrThrow()` Joiner를 사용하여 여러 작업 중 첫 번째로 성공한 결과를 반환할 수 있습니다.

```java
import java.util.concurrent.*;
import java.util.ArrayList;
import java.util.List;

public class RaceConditionExample {
    
    public static <T> T race(List<Callable<T>> tasks) throws InterruptedException {
        try (var scope = StructuredTaskScope.open(
            Joiner.anySuccessfulResultOrThrow())) {
            
            tasks.forEach(scope::fork);
            return scope.join();
            
        } catch (StructuredTaskScope.FailedException e) {
            System.err.println("모든 작업이 실패했습니다");
            return null;
        }
    }
    
    public static void main(String[] args) throws InterruptedException {
        List<Callable<String>> services = new ArrayList<>();
        
        services.add(() -> {
            Thread.sleep(1000);
            return "서버 1 응답";
        });
        
        services.add(() -> {
            Thread.sleep(500);
            return "서버 2 응답";
        });
        
        services.add(() -> {
            Thread.sleep(2000);
            return "서버 3 응답";
        });
        
        String result = race(services);
        System.out.println("결과: " + result);
    }
}
```

**실행 결과:**
```
결과: 서버 2 응답
```

## 모든 작업 결과 수집

```java
import java.util.concurrent.*;
import java.util.List;

public class CollectResultsExample {
    
    public static <T> List<T> runConcurrently(List<Callable<T>> tasks) 
            throws InterruptedException {
        try (var scope = StructuredTaskScope.open(
            Joiner.allSuccessfulOrThrow())) {
            
            tasks.forEach(scope::fork);
            return scope.join()
                       .map(Subtask::get)
                       .toList();
                       
        } catch (StructuredTaskScope.FailedException e) {
            System.err.println("작업 실패: " + e.getCause());
            return null;
        }
    }
    
    public static void main(String[] args) throws InterruptedException {
        List<Callable<Integer>> tasks = List.of(
            () -> { Thread.sleep(100); return 10; },
            () -> { Thread.sleep(200); return 20; },
            () -> { Thread.sleep(150); return 30; }
        );
        
        List<Integer> results = runConcurrently(tasks);
        System.out.println("모든 결과: " + results);
        System.out.println("합계: " + results.stream()
                                            .mapToInt(Integer::intValue)
                                            .sum());
    }
}
```

**실행 결과:**
```
모든 결과: [10, 20, 30]
합계: 60
```

## 타임아웃 설정

구조화된 동시성은 타임아웃을 쉽게 설정할 수 있습니다.

```java
import java.util.concurrent.*;
import java.time.Duration;

public class TimeoutExample {
    
    public static void main(String[] args) throws InterruptedException {
        try (var scope = StructuredTaskScope.open(
            Joiner.allSuccessfulOrThrow(),
            cf -> cf.withTimeout(Duration.ofSeconds(2)))) {
            
            scope.fork(() -> {
                Thread.sleep(1000);
                return "작업 1 완료";
            });
            
            scope.fork(() -> {
                Thread.sleep(3000); // 타임아웃 초과
                return "작업 2 완료";
            });
            
            scope.join();
            System.out.println("모든 작업 완료");
            
        } catch (StructuredTaskScope.FailedException e) {
            System.err.println("작업 실패: " + e.getCause().getClass().getSimpleName());
        }
    }
}
```

**실행 결과:**
```
작업 실패: TimeoutException
```

## 예외 처리 및 에러 전파

```java
import java.util.concurrent.StructuredTaskScope;

public class ExceptionHandlingExample {
    
    public static void main(String[] args) throws InterruptedException {
        try (var scope = StructuredTaskScope.open()) {
            
            scope.fork(() -> {
                System.out.println("작업 1 시작");
                return "작업 1 완료";
            });
            
            scope.fork(() -> {
                throw new IllegalArgumentException("유효하지 않은 인자");
            });
            
            scope.join();
            
        } catch (StructuredTaskScope.FailedException e) {
            Throwable cause = e.getCause();
            if (cause instanceof IllegalArgumentException) {
                System.err.println("유효성 검사 실패: " + cause.getMessage());
            }
        }
    }
}
```

**실행 결과:**
```
작업 1 시작
유효성 검사 실패: 유효하지 않은 인자
```

# Structured Concurrency의 핵심 이점

## 1. 명확한 작업 계층 구조
코드의 블록 구조가 작업 계층을 명확하게 표현합니다.

## 2. 자동 취소(Cancellation) 전파
한 작업이 실패하면 다른 작업들이 자동으로 취소됩니다.

## 3. 향상된 관찰성
스레드 덤프에서 작업 간의 계층 관계가 명확하게 나타납니다.

## 4. 리소스 누수 방지
try-with-resources를 통해 모든 작업이 완료될 때까지 대기합니다.

# 가상 스레드와의 결합

Structured Concurrency는 Virtual Thread(JEP 444)와 함께 사용될 때 그 진가를 발휘합니다:

```java
try (var scope = StructuredTaskScope.open()) {
    // 각 요청마다 가벼운 가상 스레드 생성
    for (int i = 0; i < 1000; i++) {
        scope.fork(() -> handleRequest(i));
    }
    scope.join();
}
```

# 주의사항

- `enable-preview` 플래그를 사용하여 컴파일 및 실행해야 함:
  ```bash
  javac --release 25 --enable-preview StructuredConcurrencyExample.java
  java --enable-preview StructuredConcurrencyExample
  ```

- `StructuredTaskScope`는 `try-with-resources`와 함께 사용되어야 함
- 작업 내에서는 인터럽트에 응답할 수 있도록 작성해야 함

# Reference

[^Java25]: [Oracle-Java_25_Release_Notes](https://docs.oracle.com/en/java/javase/25/docs/api/){:target="_blank"}
[^StructuredConcurrency]: [OpenJDK-JEP 505: Structured Concurrency (Fifth Preview)](https://openjdk.org/jeps/505){:target="_blank"}
[^VirtualThreads]: [OpenJDK-JEP 444: Virtual Threads](https://openjdk.org/jeps/444){:target="_blank"}
