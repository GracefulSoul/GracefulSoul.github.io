---
title: "Spring Cache"
excerpt: "Spring Cache에 대한 설명과 활용"
last_modified_at: 2023-11-04T13:30:00
header:
  image: /assets/images/spring/spring-cache.png
categories:
  - Spring
tags:
  - Programming
  - Spring
  - Cache

toc: true
toc_ads: true
toc_sticky: true
---
# Spring Cache[^Cache]
- Spring Cache Abstraction를 사용하여 비용이 많이 드는 메서드 수행을 반복하지 않고 데이터를 반환함으로써, 시스템 성능을 향상시킬 수 있다.
- 단, 여러 노드로 구성된 어플리케이션과 같은 Multi-Process 환경에서는 Cache Provider를 환경에 따라 구성해야 한다.

# Dependency
```xml
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context-support</artifactId>
  <version>5.3.30</version>
  <scope>compile</scope>
</dependency>
```
- 일반적으로 "spring-context-support"를 maven dependency로 추가 혹은 gradle implementation하여 사용할 수 있다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```
- Spring Boot를 사용하는 경우, "spring-boot-starter-cache"를 maven dependency로 추가 혹은 gradle implementation하면 내장되어 사용할 수 있다.

# @EnableCaching & CacheManager
```java
@EnableCaching
@Configuration
public class CacheConfiguration {

	@Bean
	public CacheManager cacheManager() {
		SimpleCacheManager cacheManager = new SimpleCacheManager();
		cacheManager.setCaches(Arrays.asList(new ConcurrentMapCache("users")));
		return cacheManager;
	}

}
```
- @EnableCaching 어노테이션을 이용하여 캐싱 기능을 활성하 하는 @Confuguration 클래스를 정의한다.
- Spring 내 캐싱 기능을 관리하는 CacheManager Bean을 설정해야 하는데, ConcurrentMapCache를 관리할 Cache 이름으로 초기화 하여 넣어준다.

# Cache Annotation
## @CacheCofig
```java
@Repository
@CacheConfig(cacheNames = "users")
public class UsersRepository {
}
```
- 클래스 전역으로 캐시에 대한 설정을 공통으로 적용하는 어노테이션이다.

## @Cacheable
```java
@Cacheable(key = "#id", unless = "#result == null")
public User select(Long id) {
  return MAP.get(id);
}
```
- 캐시를 저장하기 위한 어노테이션으로, 메서드 단위로 설정하여 key와 동일한 요청이 발생하면 캐싱된 데이터를 반환한다.

## @CachePut & @CacheEvict
```java
@CachePut(key = "#user.id")
@CacheEvict(key = "'all'")
public User update(User user) {
  MAP.put(user.getId(), user);
  return user;
}
```
- @CachePut을 사용하여 key에 해당하는 캐싱된 데이터를 요청된 값으로 변경시켜줄 수 있다.
- @CacheEvict을 사용하여 key에 해당하는 값에 대한 캐싱된 데이터를 삭제할 수 있으며, 'all'을 이용하여 전체 조회에 대한 값을 삭제하거나 allEntiries=true 설정을 이용하여 모든 데이터를 삭제할 수 있다.

## @Caching
```java
@Caching(evict = {
  @CacheEvict(key = "#id"),
  @CacheEvict(key = "'all'")
})
public boolean delete(Long id) {
  User user = MAP.remove(id);
  System.out.println(user);
  return true;
}
```
- 메서드에는 동일한 메서드를 붙일 수 없으므로 여러 캐시를 관리하기 위한 어노테이션으로, 동일한 기능 별 메서드를 그룹화하여 사용할 수 있다.

# Conclusion
- Cache는 시스템 개발에 반드시 고려해야 하는 사항으로, 서비스 운영에 지장을 주지 않을 정도의 최적화된 범위 내 적합한 읽기 / 쓰기 전략등을 활용하여 적용해야 하는 기능이다.
- 단순 Spring Cache 뿐 아니라 Redis, EhCache, 등을 통해 서비스 규모와 범위에 따라 다양한 방식으로 서비스에 Cache를 적용할 수 있다.

# Reference
[^Cache]: [Caching Data with Spring](https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/integration.html#cache){:target="_blank"}

※ Sample Code는 [여기](https://github.com/GracefulSoul/SpringCache){:target="_blank"}에서 확인 가능합니다.