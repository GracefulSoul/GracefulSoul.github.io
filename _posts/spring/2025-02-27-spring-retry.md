---
title: "Spring Retry"
excerpt: "Spring Retry에 대한 설명과 활용"
last_modified_at: 2025-02-27T13:30:00
header:
  image: /assets/images/spring/spring-retry.png
categories:
  - Spring
tags:
  - Programming
  - Spring
  - Retry

toc: true
toc_ads: true
toc_sticky: true
---
# Spring Retry[^Retry]
- Spring Project를 구성하다보면 비즈니스 로직이 정상적으로 이루어지지 않는 경우에 대한 재시도 및 오류 처리에 대한 로직을 구현할 필요가 있다.
- Spring Retry는 Spring Batch Project에서 파생되어, 현재는 분리되어 단독으로 발전해가는 프로젝트이다.

# Dependency
```xml
<dependency>
  <groupId>org.springframework.retry</groupId>
  <artifactId>spring-retry</artifactId>
  <version>2.0.11</version>
</dependency>
```
```groovy
implementation 'org.springframework.retry:spring-retry:2.0.11'
```
- 일반적으로 "spring-retry"에 대한 maven dependency로 추가 혹은 gradle implementation하여 사용할 수 있다.
- 최신 Spring Boot 프로젝트에서는 버전을 명시하지 않으면, 해당 parents에 정의된 버전으로 사용할 수 있다.

# @Retryable & @Recover
```java
@Service
public interface SqlService {

  @Retryable(retryFor = SQLException.class, maxAttempts = 3, backoff = @Backoff(delay = 100))
  void execute(String sql);

  @Recover
  void recover(SQLException e, String sql);

}
```
- @Retryable은 특정 비즈니스 로직 내 오류가 발생했을 때, 해당 메서드의 재시도를 수행할 수 있도록 정의하는 어노테이션이다.
  - retryFor는 특정 오류 상황이 발생하였을 때 재 시도 하도록 정의하는 속성이다.
  - maxAttempts는 retryFor 내 정의된 오류가 발생했을 때 최대 반복 횟수를 정의하는 속성이다.
  - backoff는 재 시도 수행 간 지연 시간을 정의하는 속성이다.
- @Recover는 @Retryable 어노테이션을 정의한 메서드가 실패하였을 경우, 최종 오류에 대한 제어 및 복구를 위해 제공되는 어노테이션이다.

```java
public interface FileService {

  @Retryable(retryFor = IOException.class, maxAttemptsExpression = "${retry.maxAttempts}", backoff = @Backoff(delayExpression = "${retry.maxDelay}"))
  void write(String path, String body);

}
```
- maxAttempts와 backoff를 application.yml 혹은 application.properties 내 정의하여 코드를 수정하지 않아도 동적으로 변경 가능하도록 하는 maxAttemptsExpression 속성과 delayExpression 속성 또한 제공된다.

# RetryTemplate
```java
@Configuration
public class RetryTemplateConfig {

  @Bean
  RetryTemplate retryTemplate(
    @Value("${retry.maxAttempts}") int maxAttempts,
    @Value("${retry.maxDelay}") long backoff
  ) {
    RetryTemplate retryTemplate = new RetryTemplate();
    FixedBackOffPolicy fixedBackOffPolicy = new FixedBackOffPolicy();
    fixedBackOffPolicy.setBackOffPeriod(backoff);
    retryTemplate.setBackOffPolicy(fixedBackOffPolicy);
    SimpleRetryPolicy retryPolicy = new SimpleRetryPolicy();
    retryPolicy.setMaxAttempts(maxAttempts);
    retryTemplate.setRetryPolicy(retryPolicy);
    retryTemplate.registerListener(new CustomRetryListener());
    return retryTemplate;
  }

}
```
- @Retryable 어노테이션 뿐 아니라, RetryTemplate을 통해서 비즈니스 수행을 원하는 정책에 따라 재시도할 수 있다.

# RetryListener
```java
public class CustomRetryListener implements RetryListener {

  public <T, E extends Throwable> void close(RetryContext context, RetryCallback<T, E> callback, Throwable throwable) {
    // Something to close.
  }

  public <T, E extends Throwable> void onError(RetryContext context, RetryCallback<T, E> callback, Throwable throwable) {
    // Something on error.
  }

  public <T, E extends Throwable> boolean open(RetryContext context, RetryCallback<T, E> callback) {
    // Something to open.
    return true;
  }

}
```
- Retry 시도에 따라 각 상황 별 추가 로깅, 비즈니스 로직들을 추가할 수 있다.
- @Retryable 어노테이션과 RetryTemplate 모두 해당 Listener를 주입하여 활용할 수 있다.

# Conclusion
- 장애 상황에 따른 복구와 대처 방안은 항상 최악의 상황을 대비할 수 있는 서비스 안정성에 기여가 된다.
- 만일 API 서비스가 Cloud 혹은 On-Premise 환경 내 API 서비스만 존재한다고 가정하면 한 환경의 장애로 서비스가 단절될 수 있지만, 이렇게 Circuit Breaker 역할을 수행할 수 있는 기능들이 존재하면 RPO(Recovery Point Objective)와 RTO(Recovery Time Objective)를 현저히 줄일 수 있을 것이다.
- 안정적인 서비스는 사용자의 편의성과 신뢰도를 바탕으로, 더욱 발전하는 서비스가 될 기회를 맞이할 것이다.

# Reference
[^Retry]: [Spring Retry Project](https://github.com/spring-projects/spring-retry){:target="_blank"}

※ Sample Code는 [여기](https://github.com/GracefulSoul/spring-cache){:target="_blank"}에서 확인 가능합니다.