---
title: "Java Design Pattern - Prototype Pattern"
excerpt: "Java를 이용하여 Design Pattern - Prototype Pattern에 대해 설명합니다."
last_modified_at: 2021-03-14T13:00:00
header:
  image: /assets/images/designpattern/creational/prototype.png
categories:
  - DesignPattern
tags:
  - Programming
	- Java
  - DesignPattern
  - Creational Patterns

toc: true
toc_ads: true
toc_sticky: true
---
# [Design Pattern](../designpattern)
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Creational Patterns, 생성 패턴
- 객체가 생성되는 방식을 중시하는 패턴이다.
- 객체의 생성과 조합을 캡슐화하여 객체가 생성 혹은 수정되어도 전체 프로그램 구조에 영향을 받지 않도록 유연성을 제공한다.

# Factory Method Pattern
- Original 객체를 새로운 객체에 복사하여 우리의 필요에 따라 수정하는 메커니즘을 제공하는 패턴이다.
- Java Cloneable 클래스의 clone() 메서드가 대표적인 예이다.

# Example
```java
public abstract class Shape implements Cloneable {

	private int id;
	protected String type;

	abstract void draw();

	public String getType() {
		return type;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public Object clone() {
		Object clone = null;
		try {
			clone = super.clone();
		} catch (CloneNotSupportedException e) {
			e.printStackTrace();
		}
		return clone;
	}

}
public class Circle extends Shape {

	public Circle() {
		type = "Circle";
	}

	@Override
	public void draw() {
		System.out.println("Inside Circle::draw() method.");
	}

}
public class Rectangle extends Shape {

	public Rectangle() {
		type = "Rectangle";
	}

	@Override
	public void draw() {
		System.out.println("Inside Rectangle::draw() method.");
	}

}
public class Square extends Shape {

	public Square() {
		type = "Square";
	}

	@Override
	public void draw() {
		System.out.println("Inside Square::draw() method.");
	}

}
public class Square extends Shape {

	public Square() {
		type = "Square";
	}

	@Override
	public void draw() {
		System.out.println("Inside Square::draw() method.");
	}

}
```

- Clonable을 상속받은 Shape Abstarct 객체를 선언하고, 하위 형태의 객체를 생성한다.

```java
public class ShapeCache {

	private static Map<Integer, Shape> shapeMap = new ConcurrentHashMap<Integer, Shape>();

	public static Shape getShape(int shapeId) {
		Shape cachedShape = shapeMap.get(shapeId);
		return (Shape) cachedShape.clone();
	}

	// For each shape run database query and create shape shapeMap.put(shapeKey, shape);
	// For example, we are adding three shapes
	public static void loadCache() {
		Circle circle = new Circle();
		circle.setId(1);
		shapeMap.put(circle.getId(), circle);

		Square square = new Square();
		square.setId(2);
		shapeMap.put(square.getId(), square);

		Rectangle rectangle = new Rectangle();
		rectangle.setId(3);
		shapeMap.put(rectangle.getId(), rectangle);
	}

}
```

- ShapeCache 객체는 Persistence Layer 대용으로 사용 할 객체이다.

```java
public class PrototypePatternMain {

	public static void main(String[] args) {
		ShapeCache.loadCache();

		Shape clonedShape = (Shape) ShapeCache.getShape(1);
		System.out.println("Shape : " + clonedShape.getType());

		Shape clonedShape2 = (Shape) ShapeCache.getShape(2);
		System.out.println("Shape : " + clonedShape2.getType());

		Shape clonedShape3 = (Shape) ShapeCache.getShape(3);
		System.out.println("Shape : " + clonedShape3.getType());
	}

}
```

- ShapeCache 객체의 getShape 메서드를 이용하여 clone된 객체를 반환함으로써, Prototype Pattern을 구현한다.

# Source
[GitHub-Prototype](https://github.com/GracefulSoul/Sample/tree/master/src/main/java/gracefulsoul/designpattern/creational/prototype)