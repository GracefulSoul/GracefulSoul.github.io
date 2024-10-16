---
title: "Java Design Pattern - Abstract Factory Pattern"
excerpt: "Java를 이용하여 Design Pattern - Abstract Factory Pattern에 대해 설명합니다."
last_modified_at: 2021-03-13T16:50:00
header:
  image: /assets/images/designpattern/creational/abstractfactory.png
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
# [Design Pattern](../designpattern){:target="_blank"}
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Creational Patterns, 생성 패턴
- 객체가 생성되는 방식을 중시하는 패턴이다.
- 객체의 생성과 조합을 캡슐화하여 객체가 생성 혹은 수정되어도 전체 프로그램 구조에 영향을 받지 않도록 유연성을 제공한다.

# Abstract Factory Pattern
- 구체적인 클래스에 의존하지 않고 서로 연관되거나 의존적인 객체들의 조합을 만들 수 있는 인터페이스를 제공하는 패턴이다.

# Example
```java
public interface Shape {

  void draw();

}
public class Circle implements Shape {

  @Override
  public void draw() {
    System.out.println("Inside Circle::draw() method.");
  }

}

public class Rectangle implements Shape {

  @Override
  public void draw() {
    System.out.println("Inside Rectangle::draw() method.");
  }

}
public class Square implements Shape {

  @Override
  public void draw() {
    System.out.println("Inside Square::draw() method.");
  }

}
public enum ShapeType {

  CIRCLE, RECTANGLE, SQUARE;

}
public interface Color {

  void fill();

}
public class Blue implements Color {

  @Override
  public void fill() {
    System.out.println("Inside Blue::fill() method.");
  }

}
public class Green implements Color {

  @Override
  public void fill() {
    System.out.println("Inside Green::fill() method.");
  }

}
public class Red implements Color {

  @Override
  public void fill() {
    System.out.println("Inside Red::fill() method.");
  }

}
public enum ColorType {

  BLUE, GREEN, RED;

}
```

- Color와 Shape의 조합을 만들 수 있는 각각의 객체를 생성한다.

```java
public abstract class AbstractFactory {

  abstract Color getColor(ColorType colorType);

  abstract Shape getShape(ShapeType shapeType);

}
public class ShapeFactory extends AbstractFactory {

  @Override
  public Shape getShape(ShapeType shapeType) {
    switch (shapeType) {
      case CIRCLE:
        return new Circle();
      case RECTANGLE:
        return new Rectangle();
      case SQUARE:
        return new Square();
      default:
        return null;
    }
  }

  @Override
  public Color getColor(ColorType colorType) {
    return null;
  }

}
public class ColorFactory extends AbstractFactory {

  @Override
  public Shape getShape(ShapeType shapeType) {
    return null;
  }

  @Override
  public Color getColor(ColorType colorType) {
    switch (colorType) {
      case RED:
        return new Red();
      case GREEN:
        return new Green();
      case BLUE:
        return new Blue();
      default:
        return null;
    }
  }

}
```

- AbstractFactory는 주어진 Color와 Shape의 조합을 만들 수 있는 인터페이스이다.
- 하위로 Color와 Shape의 세부 설정을 위한 Factory Method 객체들이 존재한다.

```java
public class FactoryProducer {

  public static AbstractFactory getFactory(FactroyType factroyType) {
    switch (factroyType) {
      case SHAPE:
        return new ShapeFactory();
      case COLOR:
        return new ColorFactory();
      default:
        return null;
    }
  }

}
public class AbstractFactoryPatternMain {

  public static void main(String[] args) {

    // Get shape factory
    AbstractFactory shapeFactory = FactoryProducer.getFactory(FactroyType.SHAPE);

    // Get an object of Shape Circle
    Shape shape1 = shapeFactory.getShape(ShapeType.CIRCLE);

    // Call draw method of Shape Circle
    shape1.draw();

    // Get an object of Shape Rectangle
    Shape shape2 = shapeFactory.getShape(ShapeType.RECTANGLE);

    // Call draw method of Shape Rectangle
    shape2.draw();

    // Get an object of Shape Square
    Shape shape3 = shapeFactory.getShape(ShapeType.SQUARE);

    // Call draw method of Shape Square
    shape3.draw();

    // Get color factory
    AbstractFactory colorFactory = FactoryProducer.getFactory(FactroyType.COLOR);

    // Get an object of Color Red
    Color color1 = colorFactory.getColor(ColorType.RED);

    // Call fill method of Red
    color1.fill();

    // Get an object of Color Green
    Color color2 = colorFactory.getColor(ColorType.GREEN);

    // Call fill method of Green
    color2.fill();

    // Get an object of Color Blue
    Color color3 = colorFactory.getColor(ColorType.BLUE);

    // Call fill method of Color Blue
    color3.fill();
  }

}
```

- FactoryProducer를 통해서 AbstractFactory 인터페이스를 가져와서 Color와 Shape의 조합을 만들 수 있다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/creational/abstractfactory){:target="_blank"}에서 확인 가능합니다.