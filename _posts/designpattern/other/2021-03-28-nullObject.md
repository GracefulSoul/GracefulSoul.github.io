---
title: "Java Design Pattern - Null Object Pattern"
excerpt: "Java를 이용하여 Design Pattern - Null Object Pattern에 대해 설명합니다."
last_modified_at: 2021-03-28T13:30:00
header:
  image: /assets/images/designpattern/other/nullObject.png
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

# Null Object Pattern
- NULL Object 인스턴스의 검사를 대체하여 사용 및 동작을 설명한다.

# Example
```java
public abstract class AbstractCustomer {

	protected String name;

	public abstract boolean isNil();

	public abstract String getName();

}
public class NullCustomer extends AbstractCustomer {

	@Override
	public String getName() {
		return "NotAvailable in Customer Database";
	}

	@Override
	public boolean isNil() {
		return true;
	}

}
public class RealCustomer extends AbstractCustomer {

	public RealCustomer(String name) {
		this.name = name;
	}

	@Override
	public String getName() {
		return name;
	}

	@Override
	public boolean isNil() {
		return false;
	}

}
```

- AbstractCustomer 인터페이스를 정의하고, 고객의 정보를 담을 수 있는 RealCustomer 클래스와 고객의 정보가 없을 때 반환할 NullCustomer 클래스를 정의한다.

```java
public class CustomerFactory {

	public static final String[] names = { "Rob", "Joe", "Julie" };

	public static AbstractCustomer getCustomer(String name) {
		for (int i = 0; i < names.length; i++) {
			if (names[i].equalsIgnoreCase(name)) {
				return new RealCustomer(name);
			}
		}
		return new NullCustomer();
	}

}
```

- 고객 정보를 보관하고 가져올 수 있는 Persistence Layer 역할을 담당할 CustomerFactory 클래스를 정의한다.

```java
public class NullPatternMain {

	public static void main(String[] args) {
		AbstractCustomer customer1 = CustomerFactory.getCustomer("Rob");
		AbstractCustomer customer2 = CustomerFactory.getCustomer("Bob");
		AbstractCustomer customer3 = CustomerFactory.getCustomer("Julie");
		AbstractCustomer customer4 = CustomerFactory.getCustomer("Laura");

		System.out.println("Customers");
		System.out.println(customer1.getName());
		System.out.println(customer2.getName());
		System.out.println(customer3.getName());
		System.out.println(customer4.getName());
	}

}
```

- CustomerFactory 클래스에 저장된 이름을 포함하여 다양한 이름으로 고객 정보를 조회해본다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/other/nullObject){:target="_blank"}에서 확인 가능합니다.