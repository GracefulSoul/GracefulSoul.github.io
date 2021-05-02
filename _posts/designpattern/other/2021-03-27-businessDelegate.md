---
title: "Java Design Pattern - Business Delegate Pattern"
excerpt: "Java를 이용하여 Design Pattern - Business Delegate Pattern에 대해 설명합니다."
last_modified_at: 2021-03-27T10:10:00
header:
  image: /assets/images/designpattern/other/businessDelegate.png
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
# [Design Pattern](../designpattern){:target="_blank"}
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Business Delegate Pattern
- Java EE 디자인 패턴이다.
- 프레젠테이션 계층과 비즈니스 계층을 분리하여 결합을 줄이고 서비스의 세부 구현 정보를 캡슐화 하는데 사용된다.
- 기본적으로 프레젠테이션 계층 코드에서 비즈니스 계층 코드에 대한 통신 또는 원격 조회 기능을 줄이는 데 사용된다.

# Example
```java
public interface BusinessService {

  public void doProcessing();

}
public class DefaultService implements BusinessService {

  @Override
  public void doProcessing() {
    System.out.println("Processing task by invoking Default Service");
  }

}
public class EJBService implements BusinessService {

  @Override
  public void doProcessing() {
    System.out.println("Processing task by invoking EJB Service");
  }

}
public class JMSService implements BusinessService {

  @Override
  public void doProcessing() {
    System.out.println("Processing task by invoking JMS Service");
  }

}
```

- BusinessService 인터페이스와 이의 구현체인 DefaultService, EJBService, JMSService를 정의한다.

```java
public enum ServiceType {
  EJB, JMS;
}
public class BusinessDelegate {

  private BusinessLookUp lookupService = new BusinessLookUp();
  private BusinessService businessService;
  private ServiceType serviceType;

  public void setServiceType(ServiceType serviceType) {
    this.serviceType = serviceType;
  }

  public void doTask() {
    businessService = lookupService.getBusinessService(serviceType);
    businessService.doProcessing();
  }

}
public class BusinessLookUp {

  public BusinessService getBusinessService(ServiceType serviceType) {
    switch (serviceType) {
      case EJB:
        return new EJBService();
      case JMS:
        return new JMSService();
      default:
        return new DefaultService();
    }
  }

}
```

- BusinessService를 특정 ServiceType에 맞게 실행 가능하도록 BusinessDelegate를 정의한다.
- BusinessLookUp 클래스는 ServiceType 별 BusinessService를 호출하는 역할을 담당한다.

```java
public class Client {

  BusinessDelegate businessDelegate;

  public Client(BusinessDelegate businessDelegate) {
    this.businessDelegate = businessDelegate;
  }

  public void doTask() {
    businessDelegate.doTask();
  }

}
```

- Client는 BusinessDelegate를 활용하여 Business를 수행할 수 있도록 구현한다.

```java
public class BusinessDelegatePatternMain {

  public static void main(String[] args) {

    BusinessDelegate businessDelegate = new BusinessDelegate();
    businessDelegate.setServiceType(ServiceType.EJB);

    Client client = new Client(businessDelegate);
    client.doTask();

    businessDelegate.setServiceType(ServiceType.JMS);
    client.doTask();
  }

}
```

- ServiceType을 변경하면서 Client의 doTask() 메서드를 호출해본다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/other/businessDelegate){:target="_blank"}에서 확인 가능합니다.