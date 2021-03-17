---
title: "Design Pattern - Flyweight Pattern이란(Java)"
excerpt: "Java를 이용하여 Design Pattern - Flyweight Pattern에 대해 설명합니다."
last_modified_at: 2021-03-17T20:40:00
header:
  image: /assets/images/designpattern/structural/flyweight.png
categories:
  - DesignPattern
tags:
  - Programming
  - DesignPattern
  - Structural Patterns

toc: true
toc_ads: true
toc_sticky: true
---
# Design Pattern[^DesignPattern]
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Structural Patterns, 구조 패턴
- 클래스와 객체를 더 큰 결과물로 합칠 수 있는 구조로 설계하는 패턴이다.
- 서로 다른 인터페이스를 지닌 여러 개의 객체를 조합하여 단일 인터페이스를 제공하거나, 객체들을 서로 묶어 새로운 기능을 제공하는 패턴이다.

# Flyweight Pattern
- 공유를 통하여 대량의 객체들을 효과적으로 지원하는 패턴이다.

# Example
```java
public interface Shape {
	void draw();
}
public class Circle implements Shape {
	private String color;
	private int x;
	private int y;
	private int radius;
	public Circle(String color) {
		this.color = color;
	}
	public void setX(int x) {
		this.x = x;
	}
	public void setY(int y) {
		this.y = y;
	}
	public void setRadius(int radius) {
		this.radius = radius;
	}
	@Override
	public void draw() {
		System.out.println("Circle: Draw() [Color : " + color + ", x : " + x + ", y :" + y + ", radius :" + radius);
	}
}
public class ShapeFactory {
	// Uncomment the compiler directive line and javac *.java will compile properly.
	// @SuppressWarnings("unchecked")
	private static final Map<String, Circle> circleMap = new HashMap<>();
	public static Shape getCircle(String color) {
		Circle circle = (Circle) circleMap.get(color);
		if (circle == null) {
			circle = new Circle(color);
			circleMap.put(color, circle);
			System.out.println("Creating circle of color : " + color);
		}
		return circle;
	}
}
```

- 공유 객체로 사용할 Shape, Circle 객체를 생성한다.
- 공유 객체를 관리하는 ShapeFactory 객체를 생성하여 color 별 첫 Circle 객체는 생성하고, 이후 요청은 circleMap에 저장된 color 별 Circle 객체를 공유하게된다.
- Javac를 활용한 Compile 시, 주석처리된 @SuppressWarnings("unchecked")을 해제하고 사용해야 정상 컴파일이 가능하다.

```java
public class FlyweightPatternMain {
	private static final String colors[] = { "Red", "Green", "Blue", "White", "Black" };
	public static void main(String[] args) {
		for (int i = 0; i < 20; ++i) {
			Circle circle = (Circle) ShapeFactory.getCircle(getRandomColor());
			circle.setX(getRandomX());
			circle.setY(getRandomY());
			circle.setRadius(100);
			circle.draw();
		}
	}
	private static String getRandomColor() {
		return colors[(int) (Math.random() * colors.length)];
	}
	private static int getRandomX() {
		return (int) (Math.random() * 100);
	}
	private static int getRandomY() {
		return (int) (Math.random() * 100);
	}
}
```

- 임의의 X축과 Y축에 반지름이 100인 원을 20개 그리도록하여 color 별 circle이 제공되는 방식을 확인한다.

# Source
[GitHub-Flyweight](https://github.com/GracefulSoul/Sample/tree/master/src/main/java/gracefulsoul/designpattern/structural/flyweight)

# Reference
[^DesignPattern]: [Blog-Design_Pattern](../designpattern)