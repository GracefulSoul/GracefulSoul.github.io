---
title: "Java Design Pattern - Intercepting Filter Pattern"
excerpt: "Java를 이용하여 Design Pattern - Intercepting Filter Pattern에 대해 설명합니다."
last_modified_at: 2021-03-28T13:30:00
header:
  image: /assets/images/designpattern/other/interceptingFilter.png
categories:
  - DesignPattern
tags:
  - Programming
  - Java
  - DesignPattern

toc: true
toc_ads: true
toc_sticky: true
---
# [Design Pattern](../designpattern)
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Intercepting Filter Pattern
- 응용 프로그램의 Request나 Response의 전/후 처리를 하고자 할 때 사용된다.
- 실제 대상 응용 프로그램에 요청을 전달하기 전에 필터가 정의되고 요청에 적용된다.
- 필터는 인증/승인/로그인 또는 요청의 추적 작업을 수행한 다음 해당 처리기에 요청을 전달할 수 있다. 

# Example
```java
public interface Filter {

	public void execute(String request);

}
public class DebugFilter implements Filter {

	public void execute(String request) {
		System.out.println("Request log: " + request);
	}

}
public class AuthenticationFilter implements Filter {

	public void execute(String request) {
		System.out.println("Authenticating request: " + request);
	}

}
```

- Filter 인터페이스를 정의하고 디버깅과 인증을 위한 DebugFilter, AuthenticationFilter 클래스를 정의한다.

```java
public class Target {

	public void execute(String request) {
		System.out.println("Executing request: " + request);
	}

}
```

- Intercepting Filter Pattern의 목표가 되는 Target 클래스를 정의한다.

```java
public class FilterChain {

	private List<Filter> filters = new ArrayList<Filter>();
	private Target target;

	public void addFilter(Filter filter) {
		filters.add(filter);
	}

	public void execute(String request) {
		for (Filter filter : filters) {
			filter.execute(request);
		}
		this.target.execute(request);
	}

	public void setTarget(Target target) {
		this.target = target;
	}

}
public class FilterManager {

	FilterChain filterChain;

	public FilterManager(Target target) {
		this.filterChain = new FilterChain();
		this.filterChain.setTarget(target);
	}

	public void setFilter(Filter filter) {
		this.filterChain.addFilter(filter);
	}

	public void filterRequest(String request) {
		this.filterChain.execute(request);
	}

}
```

- Filter를 관리하고 전처리를 하기 위한 FilterChain 클래스를 정의한다.
- 필터 처리를 관리하고 적절한 필터를 사용하여 올바른 순서로 FilterChain을 생성하고 처리를 시작하는 FilterManager 클래스를 정의한다.

```java
public class Client {

	FilterManager filterManager;

	public void setFilterManager(FilterManager filterManager) {
		this.filterManager = filterManager;
	}

	public void sendRequest(String request) {
		this.filterManager.filterRequest(request);
	}

}
```

- FilterManager를 관리하고 적용 할 수 있는 Client 클래스를 정의한다.

```java
public class InterceptingFilterMain {

	public static void main(String[] args) {
		FilterManager filterManager = new FilterManager(new Target());
		filterManager.setFilter(new AuthenticationFilter());
		filterManager.setFilter(new DebugFilter());

		Client client = new Client();
		client.setFilterManager(filterManager);
		client.sendRequest("HOME");
	}

}
```

- FilterManager 객체를 생성하여 Client 객체에 적용하여 요청을 수행해본다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/other/interceptingFilter)에서 확인 가능합니다.