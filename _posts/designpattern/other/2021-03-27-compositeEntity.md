---
title: "Java Design Pattern - Composite Entity Pattern"
excerpt: "Java를 이용하여 Design Pattern - Composite Entity Pattern에 대해 설명합니다."
last_modified_at: 2021-03-27T12:10:00
header:
  image: /assets/images/designpattern/other/compositeEntity.png
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

# Composite Entity Pattern
- EJB Persistence Mechanism에서 사용되는 디자인 패턴이다.
- Composite Entity는 객체의 그래프를 나타내는 EJB Entity Bean이다.
- Composite Entity가 업데이트되면 내부적으로 종속된 Bean이 EJB Entity에 의해 관리되어 자동으로 업데이트된다.

# Example
```java
public class DependentObject1 {

	private String data;

	public void setData(String data) {
		this.data = data;
	}

	public String getData() {
		return this.data;
	}

}
public class DependentObject2 {

	private String data;

	public void setData(String data) {
		this.data = data;
	}

	public String getData() {
		return this.data;
	}

}
```

- 종속된 Bean을 담당할 두 DependentObject1, DependentObject2를 정의한다.

```java
public class CoarseGrainedObject {

	DependentObject1 do1 = new DependentObject1();
	DependentObject2 do2 = new DependentObject2();

	public void setData(String data1, String data2) {
		do1.setData(data1);
		do2.setData(data2);
	}

	public String[] getData() {
		return new String[] { do1.getData(), do2.getData() };
	}

}
public class CompositeEntity {

	private CoarseGrainedObject cgo = new CoarseGrainedObject();

	public void setData(String data1, String data2) {
		cgo.setData(data1, data2);
	}

	public String[] getData() {
		return cgo.getData();
	}

}
```

- CoarseGrainedObject를 통해 자체 수명주기가있는 개체로 다른 개체에 대한 자체 관계를 관리한다.
- CompositeEntity는 CoarseGrainedObject이거나 CoarseGrainedObject를 참조 할 수 있는 객체이다.

```java
public class Client {

	private CompositeEntity compositeEntity = new CompositeEntity();

	public void printData() {
		for (int i = 0; i < compositeEntity.getData().length; i++) {
			System.out.println("Data: " + compositeEntity.getData()[i]);
		}
	}

	public void setData(String data1, String data2) {
		compositeEntity.setData(data1, data2);
	}

}
```

- CompositeEntity를 사용하는 Client를 정의한다.

```java
public class CompositeEntityPatternMain {

	public static void main(String[] args) {
		Client client = new Client();
		client.setData("Test", "Data");
		client.printData();

		client.setData("Second Test", "Data1");
		client.printData();
	}

}
```

- Client를 이용하여 Composite Entity Pattern을 확인한다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/other/compositeEntity)에서 확인 가능합니다.