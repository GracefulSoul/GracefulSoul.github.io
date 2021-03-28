---
title: "Java Design Pattern - Service Locator Pattern"
excerpt: "Java를 이용하여 Design Pattern - Service Locator Pattern에 대해 설명합니다."
last_modified_at: 2021-03-28T15:00:00
header:
  image: /assets/images/designpattern/other/serviceLocator.png
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

# Service Locator Pattern
- JNDI 조회를 사용하여 다양한 서비스를 찾고자 할 때 사용된다.
- 서비스에 대한 JNDI를 찾는 데 드는 높은 비용을 고려하여 캐싱 기술을 사용한다.
- Service Locator를 통한 추가 조회 또는 동일한 서비스가 캐쉬에서 수행되므로 애플리케이션 성능이 크게 향상된다.

# Example
```java
public interface Service {

	public String getName();

	public void execute();

}
public class Service1 implements Service {

	public void execute() {
		System.out.println("Executing Service1");
	}

	@Override
	public String getName() {
		return "Service1";
	}

}
public class Service2 implements Service {

	public void execute() {
		System.out.println("Executing Service2");
	}

	@Override
	public String getName() {
		return "Service2";
	}

}
```

- 다양한 서비스를 제공하기 위해 Service 인터페이스를 정의하고, Service1과 Service2 클래스를 정의한다.

```java
public class Cache {

	private List<Service> services;

	public Cache() {
		services = new ArrayList<Service>();
	}

	public Service getService(String serviceName) {
		for (Service service : services) {
			if (service.getName().equalsIgnoreCase(serviceName)) {
				System.out.println("Returning cached  " + serviceName + " object");
				return service;
			}
		}
		return null;
	}

	public void addService(Service newService) {
		boolean exists = false;
		for (Service service : services) {
			if (service.getName().equalsIgnoreCase(newService.getName())) {
				exists = true;
			}
		}
		if (!exists) {
			services.add(newService);
		}
	}
}
```

- Service들을 캐싱하여 저장 및 제공할 Cache 클래스를 정의한다.

```java
public class InitialContext {

	public Object lookup(String jndiName) {
		switch (jndiName) {
			case "SERVICE1":
				System.out.println("Looking up and creating a new Service1 object");
				return new Service1();
			case "SERVICE2":
				System.out.println("Looking up and creating a new Service2 object");
				return new Service2();
			default:
				return null;
		}
	}

}
```

- Service를 확인하여 제공할 InitialContext 클래스를 정의한다.

```java
public class ServiceLocator {

	private static Cache cache = new Cache();
	private static InitialContext context = new InitialContext();

	public static Service getService(String jndiName) {
		Service service = cache.getService(jndiName);
		if (service != null) {
			return service;
		} else {
			Service service1 = (Service) context.lookup(jndiName);
			cache.addService(service1);
			return service1;
		}
	}

}
```

- Service를 제공할 때 캐싱 기능을 사용하는 ServiceLocator 클래스를 정의한다.

```java
public class ServiceLocatorpatternMain {

	public static void main(String[] args) {
		Service service = ServiceLocator.getService("Service1");
		service.execute();
		service = ServiceLocator.getService("Service2");
		service.execute();
		service = ServiceLocator.getService("Service1");
		service.execute();
		service = ServiceLocator.getService("Service2");
		service.execute();
	}

}
```

- 정의된 각 서비스들을 호출해본다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/other/serviceLocator)에서 확인 가능합니다.