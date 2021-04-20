---
title: "Design Pattern"
excerpt: "Design Pattern에 대한 설명"
last_modified_at: 2021-03-09T19:00:00
header:
  image: /assets/images/designpattern/designpattern.png
categories:
  - DesignPattern
tags:
  - Programming
  - DesignPattern

toc: true
toc_ads: true
toc_sticky: true
---
# Design Pattern
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# 필수 요소

## Context
- 문제가 발생하는 여러 상황 기술한다.

## Problem
- 패턴이 적용되어 해결될 필요가 있는 디자인 이슈들을 기술한다. 

## Solution
- 요소들 사이의 관계, 책임, 협력등을 기술(템플릿)한다.

# GoF(Gang of Fours) 디자인 패턴 종류
- GoF(Gang of Fout)라 불리는 인에리히 감마(Erich Gamma), 리차드 헬름(Richard Helm), 랄프 존슨(Ralph Johnson), 존 블리시디스(John Vissides) 네 명의 컴퓨터 과학 연구자들이 정의하고 분류한 디자인 패턴이다.

## Creational Patterns, 생성 패턴
- 객체가 생성되는 방식을 중시하는 패턴이다.
- 객체의 생성과 조합을 캡슐화하여 객체가 생성 혹은 수정되어도 전체 프로그램 구조에 영향을 받지 않도록 유연성을 제공한다.

### [Singleton](../singleton){:target="_blank"}
- 전역 변수를 사용하지 않고 객체를 하나만 생성도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴이다.

### [Factory Method](../factory){:target="_blank"}
- 객체 생성을 서브 클래스로 분리해 처리하도록 캡슐화하는 패턴이다.

### [Abstract Factory](../abstractfactory){:target="_blank"}
- 구체적인 클래스에 의존하지 않고 서로 연관되거나 의존적인 객체들의 조합을 만들 수 있는 인터페이스를 제공하는 패턴이다.

### [Builder](../builder){:target="_blank"}
- 복잡한 객체를 생성하는 방법을 정의하는 클래스와 표현하는 방법을 정의하는 클래스를 별도로 분리하여, 서로 다른 표현이라도 이를 생성할 수 있는 동일한 절차를 제공하는 패턴이다.

### [Prototype](../prototype){:target="_blank"}
- Original 객체를 새로운 객체에 복사하여 우리의 필요에 따라 수정하는 메커니즘을 제공하는 패턴이다.
- Java Cloneable 클래스의 clone() 메서드가 대표적인 예이다.

## Structural Patterns
- 클래스와 객체를 더 큰 결과물로 합칠 수 있는 구조로 설계하는 패턴이다.
- 서로 다른 인터페이스를 지닌 여러 개의 객체를 조합하여 단일 인터페이스를 제공하거나, 객체들을 서로 묶어 새로운 기능을 제공하는 패턴이다.

### [Composite](../composite){:target="_blank"}
- 여러 개의 객체들로 구성된 복합 객체와 단일 객체를 클라이언트에서 구별 없이 다루게 해주는 패턴이다.

### [Decorator](../decorator){:target="_blank"}
- 객체의 결합을 통해 기능을 동적으로 유연하게 확장할 수 있게 해주는 패턴이다.

### [Adaptor](../adaptor){:target="_blank"}
- 클래스의 인터페이스를 사용자가 기대하는 인터페이스 형태로 변환시키는 패턴이다.

### [Proxy](../proxy){:target="_blank"}
- 어떤 다른 객체로 접근하는 것을 통제하기 위해서 그 객체의 대리자나 자리표시자의 역할을 하는 패턴이다.

### [Flyweight](../flyweight){:target="_blank"}
- 공유를 통하여 대량의 객체들을 효과적으로 지원하는 패턴이다.

### [Facade](../facade){:target="_blank"}
- 서브시스템을 더 쉽게 사용할 수 있도록 높은 수준의 인터페이스를 정의하고 제공하는 패턴이다.

### [Bridge](../bridge){:target="_blank"}
- 추상화를 구현으로부터 분리하여 각각 독립적으로 변화할 수 있도록 하는 패턴이다.

### [Filter](../filter){:target="_blank"}
- 다양한 기준을 사용하여 객체 집합을 필터링하고 논리적 작업을 통해 분리된 방식으로 연결할 수 있도록하는 패턴이다.

## Behavioral Patterns
- 객체간의 상호작용과 책임을 중시하는 패턴이다.
- 한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하면서 객체 사이의 결합도를 최소화하는 것에 중점을 두는 패턴이다.

### [Observer](../observer){:target="_blank"}
- 한 객체의 상태 변화에 따라 다른 객체의 상태도 연동되도록 일대다 객체 의존 관계를 구성하는 패턴이다.

### [State](../state){:target="_blank"}
- 객체의 상태에 따라 객체의 행위 내용을 변경하게 해주는 패턴이다.

### [Strategy](../strategy){:target="_blank"}
- 행위를 클래스로 캡슐화해 동적으로 행위를 자유롭게 바꿀 수 있게 해주는 패턴이다.

### [Command](../command){:target="_blank"}
- 실행될 기능을 캡슐화함으로써 주어진 여러 기능을 실행할 수 있는 재사용성이 높은 클래스를 설계하는 패턴이다.

### [Template Method](../template){:target="_blank"}
- 어떤 작업을 처리하는 일부분을 서브 클래스로 캡슐화하여 전체를 수행하는 구조는 바꾸지 않으면서 특정 단계에서 수행하는 작업을 바꾸는 패턴이다.

### [Interpreter](../interpreter){:target="_blank"}
- 언어 문법이나 표현을 평가할 수 있는 방법을 제공하는 패턴이다.

### [Mediator](../mediator){:target="_blank"}
- 서로 관련된 객체 사이의 복잡한 통신과 제어를 한 곳으로 집중시키는 패턴이다.

### [Memento](../memento){:target="_blank"}
- 객체를 이전의 상태로 복구시켜야 하는 경우 사용하는 패턴이다.

### [Chain of Responsibility](../chainOfResponsibility){:target="_blank"}
- 한 요청을 두 개 이상의 객체에서 처리하고 싶을 때 사용하는 패턴이다.

### [Iterator](../iterator){:target="_blank"}
- 컬렉션 구현 방법을 노출시키지 않으면서도 그 집합체 안에 들어있는 모든 항목에 접근할 수 있는 방법을 제공하는 패턴이다.

### [Visitor](../visitor){:target="_blank"}
- 알고리즘을 객체 구조에서 분리시키는 패턴이다.

## Other
- GoF 디자인 패턴 외 Java EE 등에서 사용되거나, MVC 등의 범용적인 패턴들이다.

### [Business Delegate](../businessDelegate){:target="_blank"}
- Java EE 디자인 패턴이다.
- 프레젠테이션 계층과 비즈니스 계층을 분리하여 결합을 줄이고 서비스의 세부 구현 정보를 캡슐화 하는데 사용된다.
- 기본적으로 프레젠테이션 계층 코드에서 비즈니스 계층 코드에 대한 통신 또는 원격 조회 기능을 줄이는 데 사용된다.

### [Composite Entity](../compositeEntity){:target="_blank"}
- EJB Persistence Mechanism에서 사용되는 디자인 패턴이다.
- Composite Entity는 객체의 그래프를 나타내는 EJB Entity Bean이다.
- Composite Entity가 업데이트되면 내부적으로 종속된 Bean이 EJB Entity에 의해 관리되어 자동으로 업데이트된다.

### [Data Access Object](../dataAccessObject){:target="_blank"}
- DAO 패턴이라고도 불린다.
- API 또는 작업에 액세스하는 하위 수준의 데이터를 상위 수준의 비즈니스 서비스에서 분리하는 데 사용된다.

### [Front Controller](../frontController){:target="_blank"}
- 모든 요청이 단일 핸들러로 처리되도록 중앙 집중식 요청 처리 메커니즘을 제공하는 데 사용된다.
- 이 핸들러는 요청의 인증/권한/로깅 또는 추적을 수행한 다음 요청을 해당 핸들러로 전달할 수 있다.

### [Intercepting Filter](../interceptingFilter){:target="_blank"}
- 응용 프로그램의 Request나 Response의 전/후 처리를 하고자 할 때 사용된다.
- 실제 대상 응용 프로그램에 요청을 전달하기 전에 필터가 정의되고 요청에 적용된다.
- 필터는 인증/승인/로그인 또는 요청의 추적 작업을 수행한 다음 해당 처리기에 요청을 전달할 수 있다.

### [Model-View-Controller(MVC)](../mvc){:target="_blank"}
- 사용자 인터페이스로부터 비즈니스 로직을 분리하여 애플리케이션의 시각적 요소나 그 이면에서 실행되는 비즈니스 로직을 서로 영향 없이 쉽게 고칠 수 있는 애플리케이션을 만들 기 위해 사용한다.

### [Null Object](../nullObject){:target="_blank"}
- NULL Object 인스턴스의 검사를 대체하여 사용 및 동작을 설명한다.

### [Service Locator](../serviceLocator){:target="_blank"}
- JNDI 조회를 사용하여 다양한 서비스를 찾고자 할 때 사용된다.
- 서비스에 대한 JNDI를 찾는 데 드는 높은 비용을 고려하여 캐싱 기술을 사용한다.
- Service Locator를 통한 추가 조회 또는 동일한 서비스가 캐쉬에서 수행되므로 애플리케이션 성능이 크게 향상된다.

### Transfer Object(../transferObject){:target="_blank"}
- 여러 속성을 가진 데이터를 Client에서 Server로 한 번에 전달할 때 사용된다.