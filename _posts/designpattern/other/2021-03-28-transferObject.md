---
title: "Java Design Pattern - Transfer Object Pattern"
excerpt: "Java를 이용하여 Design Pattern - Transfer Object Pattern에 대해 설명합니다."
last_modified_at: 2021-03-28T15:00:00
header:
  image: /assets/images/designpattern/other/transferObject.png
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

# Transfer Object Pattern
- 여러 속성을 가진 데이터를 Client에서 Server로 한 번에 전달할 때 사용된다.

# Example
```java
public class StudentVO {

  private String name;
  private int rollNo;

  StudentVO(String name, int rollNo) {
    this.name = name;
    this.rollNo = rollNo;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public int getRollNo() {
    return rollNo;
  }

  public void setRollNo(int rollNo) {
    this.rollNo = rollNo;
  }

}
```

- Value Object 역할을 수행할 StudentVO 클래스를 정의한다.

```java
public class StudentBO {

  // List is working as a database.
  List<StudentVO> students;

  public StudentBO() {
    students = new ArrayList<StudentVO>();
    StudentVO student1 = new StudentVO("Robert", 0);
    StudentVO student2 = new StudentVO("John", 1);
    students.add(student1);
    students.add(student2);
  }

  public void deleteStudent(StudentVO student) {
    students.remove(student.getRollNo());
    System.out.println("Student: Roll No " + student.getRollNo() + ", deleted from database");
  }

  // Retrieve list of student from the database.
  public List<StudentVO> getAllStudents() {
    return students;
  }

  public StudentVO getStudent(int rollNo) {
    return students.get(rollNo);
  }

  public void updateStudent(StudentVO student) {
    students.get(student.getRollNo());
    System.out.println("Student: Roll No " + student.getRollNo() + ", updated from database");
  }

}
```

- Business Object 역할을 담당하는 StudentBO 클래스를 정의한다.

```java
public class TransferObjectPatternMain {

  public static void main(String[] args) {
    StudentBO studentBusinessObject = new StudentBO();

    // Print all students.
    for (StudentVO student : studentBusinessObject.getAllStudents()) {
      System.out.println("Student: [RollNo : " + student.getRollNo() + ", Name : " + student.getName() + " ]");
    }

    // Update student.
    StudentVO student = studentBusinessObject.getAllStudents().get(0);
    student.setName("Michael");
    studentBusinessObject.updateStudent(student);

    // Get the student.
    student = studentBusinessObject.getStudent(0);
    System.out.println("Student: [RollNo : " + student.getRollNo() + ", Name : " + student.getName() + " ]");
  }

}
```

- StudentBO 객체를 사용하여 StudentVO를 조회 및 수정을 해본다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/other/transferObject){:target="_blank"}에서 확인 가능합니다.