---
title: "Java 26 - HTTP/3 for the HTTP Client API"
excerpt: "Java 26에서 HTTP/3 프로토콜이 HTTP Client API에 추가되었습니다"
last_modified_at: 2026-03-17T10:00:00
header:
  image: /assets/images/java/java.png
categories:
  - Java
tags:
  - Programming
  - Releases
  - Java 26
  - HTTP/3
  - Networking

toc: true
toc_ads: true
toc_sticky: true
---

# JAVA 26[^Java26]

Java 26에서는 HTTP Client[^Http3ClientAPI] API에 HTTP/3[^HTTP3Spec] 프로토콜 지원이 추가되었습니다. HTTP/3는 UDP 기반의 QUIC 프로토콜[^QUICSpec]을 사용하여 더 빠른 핸드셰이크, 낮은 지연시간, 그리고 높은 패킷 손실 환경에서의 더 안정적인 전송을 제공합니다.

## HTTP/3의 장점

- **빠른 연결 수립**: 0-RTT(Round Trip Time) 핸드셰이크 지원
- **머리-줄-세우기 차단 제거**: 독립적인 스트림 처리로 병렬 요청 효율 증가
- **네트워크 마이그레이션**: WiFi에서 LTE로 전환 시 연결 유지
- **더 안정적인 전송**: 패킷 손실이 많은 환경에서 우수한 성능

## 기본 사용법

### 1. HttpClient에서 HTTP/3 활성화

```java
import java.net.http.*;
import java.net.URI;

public class BasicHttp3Example {
    
    public static void main(String[] args) throws Exception {
        // HTTP/3을 사용하도록 설정
        HttpClient client = HttpClient.newBuilder()
            .version(HttpClient.Version.HTTP_3)
            .build();
        
        HttpRequest request = HttpRequest.newBuilder(
            URI.create("https://httpbin.org/get")
        )
            .GET()
            .build();
        
        HttpResponse<String> response = client.send(
            request,
            HttpResponse.BodyHandlers.ofString()
        );
        
        System.out.println("상태 코드: " + response.statusCode());
        System.out.println("버전: " + response.version());
        System.out.println("응답 길이: " + response.body().length());
    }
}
```

**실행 결과:**
```
상태 코드: 200
버전: HTTP_3
응답 길이: 425
```

## 요청별 버전 지정

### 2. 개별 요청에 HTTP/3 적용

```java
import java.net.http.*;
import java.net.URI;

public class Http3PerRequestExample {
    
    public static void main(String[] args) throws Exception {
        // 클라이언트는 HTTP/2 기본값 유지
        HttpClient client = HttpClient.newHttpClient();
        
        // 특정 요청에서만 HTTP/3 사용
        HttpRequest request = HttpRequest.newBuilder(
            URI.create("https://api.example.com/data")
        )
            .version(HttpClient.Version.HTTP_3)
            .GET()
            .build();
        
        HttpResponse<String> response = client.send(
            request,
            HttpResponse.BodyHandlers.ofString()
        );
        
        System.out.println("응답 버전: " + response.version());
        System.out.println("상태: " + response.statusCode());
    }
}
```

## HTTP/3 프로토콜 협상

### 3. 자동 프토토콜 다운그레이드

```java
import java.net.http.*;
import java.net.URI;

public class Http3AutoDowngradeExample {
    
    public static void sendWithFallback(String url) throws Exception {
        HttpClient client = HttpClient.newBuilder()
            .version(HttpClient.Version.HTTP_3)
            .build();
        
        HttpRequest request = HttpRequest.newBuilder(
            URI.create(url)
        )
            .GET()
            .build();
        
        try {
            HttpResponse<String> response = client.send(
                request,
                HttpResponse.BodyHandlers.ofString()
            );
            
            System.out.println("URL: " + url);
            System.out.println("사용된 프로토콜: " + response.version());
            System.out.println("상태: " + response.statusCode());
            
        } catch (Exception e) {
            System.err.println("요청 실패: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) throws Exception {
        // HTTP/3을 지원하는 서버
        sendWithFallback("https://www.google.com");
        
        // HTTP/3을 지원하지 않으면 자동으로 HTTP/2로 다운그레이드
        sendWithFallback("https://api.example.com/old-server");
    }
}
```

## 병렬 요청

### 4. 여러 요청을 HTTP/3으로 동시 실행

```java
import java.net.http.*;
import java.net.URI;
import java.util.concurrent.CompletableFuture;
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class Http3ParallelRequestsExample {
    
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newBuilder()
            .version(HttpClient.Version.HTTP_3)
            .build();
        
        List<String> urls = Arrays.asList(
            "https://httpbin.org/uuid",
            "https://httpbin.org/user-agent",
            "https://httpbin.org/headers"
        );
        
        // 비동기 요청 생성
        List<CompletableFuture<HttpResponse<String>>> futures = urls.stream()
            .map(url -> {
                HttpRequest request = HttpRequest.newBuilder(
                    URI.create(url)
                )
                    .GET()
                    .build();
                
                return client.sendAsync(
                    request,
                    HttpResponse.BodyHandlers.ofString()
                );
            })
            .collect(Collectors.toList());
        
        // 모든 요청이 완료될 때까지 대기
        CompletableFuture<Void> allFutures = 
            CompletableFuture.allOf(futures.toArray(new CompletableFuture[0]));
        
        allFutures.thenRun(() -> {
            System.out.println("모든 요청 완료:");
            futures.forEach(f -> {
                try {
                    HttpResponse<String> response = f.join();
                    System.out.println("상태: " + response.statusCode() + 
                                     ", 프로토콜: " + response.version());
                } catch (Exception e) {
                    e.printStackTrace();
                }
            });
        }).join();
    }
}
```

**실행 결과:**
```
모든 요청 완료:
상태: 200, 프로토콜: HTTP_3
상태: 200, 프로토콜: HTTP_3
상태: 200, 프로토콜: HTTP_3
```

## Alternative Services 발견

### 5. HTTP Alternative Services (Alt-Svc) 사용

```java
import java.net.http.*;
import java.net.URI;

public class Http3AltSvcExample {
    
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newBuilder()
            .version(HttpClient.Version.HTTP_2)  // 첫 요청은 HTTP/2
            .build();
        
        // 첫 번째 요청: HTTP/2로 시작하지만 Alt-Svc 헤더 수신
        HttpRequest request1 = HttpRequest.newBuilder(
            URI.create("https://api.example.com/resource")
        )
            .GET()
            .build();
        
        HttpResponse<String> response1 = client.send(
            request1,
            HttpResponse.BodyHandlers.ofString()
        );
        
        System.out.println("첫 번째 요청:");
        System.out.println("프로토콜: " + response1.version());
        System.out.println("Alt-Svc: " + response1.headers()
            .firstValue("alt-svc")
            .orElse("없음"));
        
        // 두 번째 요청: 같은 서버에 대해 HTTP/3 지원이 감지되었으면 사용
        HttpRequest request2 = HttpRequest.newBuilder(
            URI.create("https://api.example.com/data")
        )
            .version(HttpClient.Version.HTTP_3)
            .GET()
            .build();
        
        HttpResponse<String> response2 = client.send(
            request2,
            HttpResponse.BodyHandlers.ofString()
        );
        
        System.out.println("\n두 번째 요청:");
        System.out.println("프로토콜: " + response2.version());
    }
}
```

## POST 요청과 본문 전송

### 6. HTTP/3로 POST 요청

```java
import java.net.http.*;
import java.net.URI;
import java.nio.charset.StandardCharsets;

public class Http3PostExample {
    
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newBuilder()
            .version(HttpClient.Version.HTTP_3)
            .build();
        
        String jsonPayload = """
            {
                "name": "John",
                "email": "john@example.com",
                "age": 30
            }
            """;
        
        HttpRequest request = HttpRequest.newBuilder(
            URI.create("https://api.example.com/users")
        )
            .header("Content-Type", "application/json")
            .POST(HttpRequest.BodyPublishers.ofString(jsonPayload))
            .build();
        
        HttpResponse<String> response = client.send(
            request,
            HttpResponse.BodyHandlers.ofString()
        );
        
        System.out.println("상태 코드: " + response.statusCode());
        System.out.println("프로토콜: " + response.version());
        System.out.println("응답: " + response.body());
    }
}
```

## 에러 처리와 타임아웃

### 7. HTTP/3 요청의 에러 처리

```java
import java.net.http.*;
import java.net.URI;
import java.time.Duration;

public class Http3ErrorHandlingExample {
    
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newBuilder()
            .version(HttpClient.Version.HTTP_3)
            .connectTimeout(Duration.ofSeconds(5))
            .build();
        
        HttpRequest request = HttpRequest.newBuilder(
            URI.create("https://api.example.com/timeout")
        )
            .timeout(Duration.ofSeconds(5))
            .GET()
            .build();
        
        try {
            HttpResponse<String> response = client.send(
                request,
                HttpResponse.BodyHandlers.ofString()
            );
            
            // 상태 코드 확인
            if (response.statusCode() >= 400) {
                System.err.println("오류: 상태 코드 " + response.statusCode());
                System.err.println("응답: " + response.body());
            } else {
                System.out.println("성공: " + response.statusCode());
            }
            
        } catch (java.net.http.HttpTimeoutException e) {
            System.err.println("타임아웃: " + e.getMessage());
        } catch (java.io.IOException e) {
            System.err.println("네트워크 오류: " + e.getMessage());
        } catch (InterruptedException e) {
            System.err.println("중단됨: " + e.getMessage());
            Thread.currentThread().interrupt();
        }
    }
}
```

## 응답 헤더 및 메타데이터

### 8. HTTP/3 응답 정보 확인

```java
import java.net.http.*;
import java.net.URI;
import java.util.List;
import java.util.Map;

public class Http3ResponseMetadataExample {
    
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newBuilder()
            .version(HttpClient.Version.HTTP_3)
            .build();
        
        HttpRequest request = HttpRequest.newBuilder(
            URI.create("https://httpbin.org/response-headers")
        )
            .GET()
            .build();
        
        HttpResponse<String> response = client.send(
            request,
            HttpResponse.BodyHandlers.ofString()
        );
        
        System.out.println("=== 응답 정보 ===");
        System.out.println("상태 코드: " + response.statusCode());
        System.out.println("버전: " + response.version());
        System.out.println("URI: " + response.request().uri());
        
        System.out.println("\n=== 헤더 ===");
        response.headers().map().forEach((name, values) -> {
            System.out.println(name + ": " + String.join(", ", values));
        });
        
        System.out.println("\n=== 본문 크기 ===");
        System.out.println("크기: " + response.body().length() + " bytes");
    }
}
```

**실행 결과:**
```
=== 응답 정보 ===
상태 코드: 200
버전: HTTP_3
URI: https://httpbin.org/response-headers

=== 헤더 ===
content-type: application/json
content-length: 123
server: gunicorn/19.9.0

=== 본문 크기 ===
크기: 123 bytes
```

# HTTP/3 마이그레이션 가이드

## 기존 HTTP/2 코드

```java
// 기존 HTTP/2 코드
HttpClient client = HttpClient.newHttpClient();
```

## HTTP/3으로 마이그레이션

```java
// HTTP/3 사용
HttpClient client = HttpClient.newBuilder()
    .version(HttpClient.Version.HTTP_3)
    .build();

// 또는 자동 다운그레이드와 함께
HttpClient client = HttpClient.newBuilder()
    .version(HttpClient.Version.HTTP_3)
    .build();
```

# 주요 특징

| 기능 | 설명 |
|------|------|
| **자동 다운그레이드** | HTTP/3 미지원 시 자동으로 HTTP/2 또는 HTTP/1.1로 변경 |
| **기본값 유지** | 기본 버전은 여전히 HTTP/2 (선택적 HTTP/3) |
| **API 호환성** | 기존 코드 수정 최소화 |
| **성능** | 더 빠른 핸드셰이크, 낮은 지연시간 |

# 주의사항

1. **선택적 사용**: HTTP/3은 기본이 아니므로 명시적으로 활성화 필요
2. **서버 지원**: 모든 서버가 HTTP/3을 지원하지는 않음
3. **파이어월**: 일부 방화벽이 QUIC(UDP 포트 443) 차단 가능
4. **모니터링**: HTTP/3 요청의 실패를 처리할 수 있도록 구현

# 성능 개선 예상 효과

- **연결 수립 시간**: 50-90% 감소
- **페이지 로드 시간**: 10-30% 감소
- **네트워크 복구**: 패킷 손실 환경에서 우수

# Reference

[^Java26]: [Oracle-Java_26_Release_Notes](https://docs.oracle.com/en/java/javase/26/docs/api/){:target="_blank"}
[^Http3ClientAPI]: [OpenJDK-JEP 517: HTTP/3 for the HTTP Client API](https://openjdk.org/jeps/517){:target="_blank"}
[^HTTP3Spec]: [RFC 9114: HTTP/3](https://www.rfc-editor.org/rfc/rfc9114){:target="_blank"}
[^QUICSpec]: [RFC 9000: QUIC Protocol](https://www.rfc-editor.org/rfc/rfc9000){:target="_blank"}
