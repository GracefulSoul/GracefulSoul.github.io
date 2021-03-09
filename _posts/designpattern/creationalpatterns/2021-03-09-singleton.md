---
title: "Design Pattern - Singleton Pattern이란"
excerpt: "Design Pattern에 - Singleton Pattern에 대한 설명"
last_modified_at: 2021-03-09T19:00:00
header:
  image: /assets/images/designpattern/designpattern.png
categories:
  - Paradigm
tags:
  - Programming
  - Design Pattern
  - Creational Patterns

toc: true
toc_ads: true
toc_sticky: true
---
# Creational Patterns, 생성 패턴
- 객체가 생성되는 방식을 중시하는 패턴이다.
- 객체의 생성과 조합을 캡슐화하여 객체가 생성 혹은 수정되어도 전체 프로그램 구조에 영향을 받지 않도록 유연성을 제공한다.

# Singleton Pattern
- 전역 변수를 사용하지 않고 객체를 하나만 생성도록 하며, 생성된 객체를 어디에서든지 참조할 수 있도록 하는 패턴이다.

# Sample
```java
public class SingleObject {
	// Create an object of SingleObject.
	private static SingleObject instance = new SingleObject();
	// Make the constructor private so that this class cannot be instantiated.
	private SingleObject() {
	}
	// Get the only object available.
	public static SingleObject getInstance() {
		return instance;
	}
	public void showMessage() {
		System.out.println("Hello World!");
	}
}
```

- private 생성자만 구현함으로써, 외부에서 해당 객체를 생성하지 못하도록 하였다.
- 하나의 객체를 생성하여 getter method를 제공함으로써, 해당 객체를 다른 객체에서 참조 가능하도록 하였다.

```java
public class SingletonPatternMain {
	public static void main(String[] args) {
		// Illegal construct.
		// Compile Time Error: The constructor SingleObject() is not visible.
		// SingleObject object = new SingleObject();
		// Get the only object available.
		SingleObject object = SingleObject.getInstance();
		// Show the message.
		object.showMessage();
	}
}
```

- Singleton 객체를 생성자를 통해 생성하고자 하면, Compile 단계에서 오류가 발생한다.
- Singleton 객체의 getter 메서드를 이용하여 내부 메서드(기능)를 사용하면 정상적으로 수행이 된다.