---
title: "Java Design Pattern - Decorator Pattern"
excerpt: "Java를 이용하여 Design Pattern - Decorator Pattern에 대해 설명합니다."
last_modified_at: 2021-03-14T15:30:00
header:
  image: /assets/images/designpattern/structural/decorator.png
categories:
  - DesignPattern
tags:
  - Programming
  - Java
  - DesignPattern
  - Structural Patterns

toc: true
toc_ads: true
toc_sticky: true
---
# [Design Pattern](../designpattern)
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Structural Patterns, 구조 패턴
- 클래스와 객체를 더 큰 결과물로 합칠 수 있는 구조로 설계하는 패턴이다.
- 서로 다른 인터페이스를 지닌 여러 개의 객체를 조합하여 단일 인터페이스를 제공하거나, 객체들을 서로 묶어 새로운 기능을 제공하는 패턴이다.

# Decorator Pattern
- 객체의 결합을 통해 기능을 동적으로 유연하게 확장할 수 있게 해주는 패턴이다.

# Example
```java
public interface Shape {

  void draw();

}
public class Circle implements Shape {

  @Override
  public void draw() {
    System.out.println("Shape: Circle");
  }

}
public class Rectangle implements Shape {

  @Override
  public void draw() {
    System.out.println("Shape: Rectangle");
  }

}
```

- 각 도형을 그리기 위해 Shape 인터페이스를 정의하고, Circle, Rectangle 클래스를 구현하여 draw() 메서드를 작성한다.

```java
public abstract class ShapeDecorator implements Shape {

  protected Shape decoratedShape;

  public ShapeDecorator(Shape decoratedShape) {
    this.decoratedShape = decoratedShape;
  }

  public void draw() {
    decoratedShape.draw();
  }

}
public class RedShapeDecorator extends ShapeDecorator {

  public RedShapeDecorator(Shape decoratedShape) {
    super(decoratedShape);
  }

  @Override
  public void draw() {
    decoratedShape.draw();
    setRedBorder(decoratedShape);
  }

  private void setRedBorder(Shape decoratedShape) {
    System.out.println("Border Color: Red");
  }

}
```

- Shape 인터페이스를 단순 상속받은 Circle, Rectangle 객체는 단순 형태를 그릴 수 있지만, Decorator Pattern을 활용하여 색상을 추가하였다.

```java
public class DecoratorPatternMain {

  public static void main(String[] args) {
    Shape circle = new Circle();
    Shape redCircle = new RedShapeDecorator(new Circle());
    Shape redRectangle = new RedShapeDecorator(new Rectangle());

    System.out.println("Circle with normal border");
    circle.draw();

    System.out.println("Circle of red border");
    redCircle.draw();

    System.out.println("Rectangle of red border");
    redRectangle.draw();
  }

}
```

- Shape의 형태 별 객체와 Decorator 객체를 이용하여 확인한다.

# Source
[GitHub-Decorator](https://github.com/GracefulSoul/Sample/tree/master/src/main/java/gracefulsoul/designpattern/structural/decorator)