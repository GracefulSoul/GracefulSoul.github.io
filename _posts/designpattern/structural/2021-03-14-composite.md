---
title: "Java Design Pattern - Composite Pattern"
excerpt: "Java를 이용하여 Design Pattern - Composite Pattern에 대해 설명합니다."
last_modified_at: 2021-03-14T15:30:00
header:
  image: /assets/images/designpattern/structural/composite.png
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
# [Design Pattern](../designpattern){:target="_blank"}
- 과거의 소프트웨어 개발 과정에서 발견된 설계의 노하우를 축적하여 이름을 붙여, 이후에 재이용하기 좋은 형태로 특정의 규약을 묶어서 정리한 것이다.
- 디자인 패턴은 알고리즘이 아니라 상황에 따라 자주 쓰이는 설계 방법을 정리한 코딩 방법론일 뿐이며 모든 상황의 해결책이 아니다.

# Structural Patterns, 구조 패턴
- 클래스와 객체를 더 큰 결과물로 합칠 수 있는 구조로 설계하는 패턴이다.
- 서로 다른 인터페이스를 지닌 여러 개의 객체를 조합하여 단일 인터페이스를 제공하거나, 객체들을 서로 묶어 새로운 기능을 제공하는 패턴이다.

# Composite Pattern
- 여러 개의 객체들로 구성된 복합 객체와 단일 객체를 클라이언트에서 구별 없이 다루게 해주는 패턴이다.

# Example
```java
public class Employee {

  private String name;
  private String dept;
  private int salary;
  private List<Employee> subordinates;

  // Constructor
  public Employee(String name, String dept, int sal) {
    this.name = name;
    this.dept = dept;
    this.salary = sal;
    this.subordinates = new ArrayList<Employee>();
  }

  public void add(Employee e) {
    this.subordinates.add(e);
  }

  public void remove(Employee e) {
    this.subordinates.remove(e);
  }

  public List<Employee> getSubordinates() {
    return this.subordinates;
  }

  public String toString() {
    return ("Employee :[ Name : " + this.name + ", dept : " + this.dept + ", salary :" + this.salary + " ]");
  }

}
```

- 다양한 직급의 임직원 정보를 저장할 Employee 객체를 생성한다.

```java
public class CompositePatternMain {

  public static void main(String[] args) {
    Employee CEO = new Employee("John", "CEO", 30000);

    Employee headSales = new Employee("Robert", "Head Sales", 20000);
    Employee headMarketing = new Employee("Michel", "Head Marketing", 20000);

    Employee clerk1 = new Employee("Laura", "Marketing", 10000);
    Employee clerk2 = new Employee("Bob", "Marketing", 10000);

    Employee salesExecutive1 = new Employee("Richard", "Sales", 10000);
    Employee salesExecutive2 = new Employee("Rob", "Sales", 10000);

    CEO.add(headSales);
    CEO.add(headMarketing);

    headSales.add(salesExecutive1);
    headSales.add(salesExecutive2);

    headMarketing.add(clerk1);
    headMarketing.add(clerk2);

    // Print all employees of the organization.
    System.out.println(CEO);

    for (Employee headEmployee : CEO.getSubordinates()) {
      System.out.println(headEmployee);
      for (Employee employee : headEmployee.getSubordinates()) {
        System.out.println(employee);
      }
    }

  }
}
```

- CEO부터 영업직군까지 Employee를 추가하여 CEO와 subordinates에 포함된 모든 임직원들을 출력한다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/structural/composite){:target="_blank"}에서 확인 가능합니다.