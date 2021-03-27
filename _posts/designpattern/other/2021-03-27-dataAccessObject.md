---
title: "Java Design Pattern - Data Access Object Pattern"
excerpt: "Java를 이용하여 Design Pattern - Data Access Object Pattern에 대해 설명합니다."
last_modified_at: 2021-03-27T13:30:00
header:
  image: /assets/images/designpattern/other/dataAccessObject.png
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

# Data Access Object Pattern
- DAO 패턴이라고도 불린다.
- API 또는 작업에 액세스하는 하위 수준의 데이터를 상위 수준의 비즈니스 서비스에서 분리하는 데 사용된다.

# Example
```java
public class Student {

	private String name;
	private int rollNo;

	Student(String name, int rollNo) {
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

- Student DTO객체를 정의한다.

```java
public interface StudentDao {

	public List<Student> getAllStudents();

	public Student getStudent(int rollNo);

	public void updateStudent(Student student);

	public void deleteStudent(Student student);

}
public class StudentDaoImpl implements StudentDao {

	// List is working as a database.
	List<Student> students;

	public StudentDaoImpl() {
		students = new ArrayList<Student>();
		Student student1 = new Student("Robert", 0);
		Student student2 = new Student("John", 1);
		students.add(student1);
		students.add(student2);
	}

	@Override
	public void deleteStudent(Student student) {
		students.remove(student.getRollNo());
		System.out.println("Student: Roll No " + student.getRollNo() + ", deleted from database");
	}

	// Retrieve list of students from the database.
	@Override
	public List<Student> getAllStudents() {
		return students;
	}

	@Override
	public Student getStudent(int rollNo) {
		return students.get(rollNo);
	}

	@Override
	public void updateStudent(Student student) {
		students.get(student.getRollNo()).setName(student.getName());
		System.out.println("Student: Roll No " + student.getRollNo() + ", updated in the database");
	}

}
```

- Student 관련 기능을 제공할 StudentDao 인터페이스를 정의하고, 세부 기능을 구현한 StudentDaoImpl 클래스를 정의한다.

```java
public class DaoPatternMain {

	public static void main(String[] args) {
		StudentDao studentDao = new StudentDaoImpl();

		// Print all students.
		for (Student student : studentDao.getAllStudents()) {
			System.out.println("Student: [RollNo : " + student.getRollNo() + ", Name : " + student.getName() + " ]");
		}

		// Update student.
		Student student = studentDao.getAllStudents().get(0);
		student.setName("Michael");
		studentDao.updateStudent(student);

		// Get the student.
		studentDao.getStudent(0);
		System.out.println("Student: [RollNo : " + student.getRollNo() + ", Name : " + student.getName() + " ]");
	}

}
```

- StudentDao를 활용하여 기능을 수행해본다.

# Source
Sample Code는 [여기](https://github.com/GracefulSoul/designpattern/tree/master/src/main/java/gracefulsoul/other/dataAccessObject)에서 확인 가능합니다.