---
title: "Java Design Pattern - Interpreter Pattern"
excerpt: "Java를 이용하여 Design Pattern - Interpreter Pattern에 대해 설명합니다."
last_modified_at: 2021-03-20T10:40:00
header:
  image: /assets/images/designpattern/behavioral/interpreter.png
categories:
  - DesignPattern
tags:
  - Programming
  - Java
  - DesignPattern
  - Behavioral Patterns

toc: true
toc_ads: true
toc_sticky: true
---
# [Design Pattern](../designpattern)
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Behavioral Patterns, 행위 패턴
- 객체간의 상호작용과 책임을 중시하는 패턴이다.
- 한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하면서 객체 사이의 결합도를 최소화하는 것에 중점을 두는 패턴이다.

# Interpreter Pattern
- 언어 문법이나 표현을 평가할 수 있는 방법을 제공하는 패턴이다. 

# Example
```java
public interface Expression {

  public boolean interpret(String context);

}
public class AndExpression implements Expression {

  private Expression expr1 = null;
  private Expression expr2 = null;

  public AndExpression(Expression expr1, Expression expr2) {
    this.expr1 = expr1;
    this.expr2 = expr2;
  }

  @Override
  public boolean interpret(String context) {
    return expr1.interpret(context) && expr2.interpret(context);
  }

}
public class OrExpression implements Expression {

  private Expression expr1 = null;
  private Expression expr2 = null;

  public OrExpression(Expression expr1, Expression expr2) {
    this.expr1 = expr1;
    this.expr2 = expr2;
  }

  @Override
  public boolean interpret(String context) {
    return expr1.interpret(context) || expr2.interpret(context);
  }

}
public class TerminalExpression implements Expression {

  private String data;

  public TerminalExpression(String data) {
    this.data = data;
  }

  @Override
  public boolean interpret(String context) {
    if (context.contains(data)) {
      return true;
    }
    return false;
  }

}
```

- 각 표현식을 위해 Interpreter 인터페이스를 정의한다.
- And, Or 표현을 위해 각 Expression 객체를 구현하고, 데이터를 주입받아 각 Expression에 주입할 TerminalExpression 객체를 구현한다.

```java
public class InterpreterPatternMain {

  // Rule: Robert and John are male
  public static Expression getMaleExpression() {
    Expression robert = new TerminalExpression("Robert");
    Expression john = new TerminalExpression("John");
    return new OrExpression(robert, john);
  }

  // Rule: Julie is a married women
  public static Expression getMarriedWomanExpression() {
    Expression julie = new TerminalExpression("Julie");
    Expression married = new TerminalExpression("Married");
    return new AndExpression(julie, married);
  }

  public static void main(String[] args) {
    Expression isMale = getMaleExpression();
    Expression isMarriedWoman = getMarriedWomanExpression();

    System.out.println("John is male? " + isMale.interpret("John"));
    System.out.println("Julie is a married women? " + isMarriedWoman.interpret("Married Julie"));
  }

}
```

- Expression의 조합을 통해서 각 질의를 수행해본다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/behavioral/interpreter)에서 확인 가능합니다.