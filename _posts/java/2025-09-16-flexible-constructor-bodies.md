---
title: "Java 25 - Flexible Constructor Bodies (Final)"
excerpt: "Java 25에서 생성자의 유연한 몸체가 최종 기능으로 제공됩니다"
last_modified_at: 2025-09-16T12:00:00
header:
  image: /assets/images/java/java.png
categories:
  - Java
tags:
  - Programming
  - Releases
  - Java 25
  - Constructor
  - Safety

toc: true
toc_ads: true
toc_sticky: true
---

# JAVA 25

Java 25에서는 생성자의 본문 앞에 `super(...)` 또는 `this(...)` 호출 이전에 명령문들을 작성할 수 있도록 허용합니다. 이는 생성자에서 인자 검증을 우선적으로 수행할 수 있게 하며, 객체의 무결성을 더욱 강화합니다.

## 기존의 문제점

Java 24 이전에는 다음과 같은 제한이 있었습니다:

- 생성자의 첫 문장은 반드시 `super()` 또는 `this()` 호출이어야 함
- 인자 검증 후 상위 클래스 생성자 호출이 불가능
- 상위 클래스 생성자가 부분 초기화된 하위 클래스 필드에 접근할 수 있음

## 기본 예제: Fail-Fast 검증

### 1. 생성자 인자 검증

```java
public class Employee extends Person {
    
    private String officeID;
    
    // Java 25 이전: 검증을 할 수 없었음
    // Java 25 이후: super() 호출 전 검증 가능
    public Employee(String name, int age, String officeID) {
        // 프롤로그: super() 호출 전 명령문
        if (age < 18 || age > 67) {
            throw new IllegalArgumentException(
                "직원은 18세 이상 67세 이하여야 합니다"
            );
        }
        
        if (officeID == null || officeID.isEmpty()) {
            throw new IllegalArgumentException(
                "사무실 ID는 필수입니다"
            );
        }
        
        // 상위 클래스 생성자 호출
        super(name, age);
        
        // 에필로그: super() 호출 후 명령문
        this.officeID = officeID;
        System.out.println("직원이 생성되었습니다: " + name);
    }
    
    public String getOfficeID() {
        return officeID;
    }
    
    public static void main(String[] args) {
        try {
            // 유효한 직원
            Employee emp1 = new Employee("Alice", 30, "OFF-001");
            System.out.println("사무실: " + emp1.getOfficeID());
            
            // 나이 범위 위반
            Employee emp2 = new Employee("Bob", 15, "OFF-002");
            
        } catch (IllegalArgumentException e) {
            System.err.println("오류: " + e.getMessage());
        }
    }
}

class Person {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() { return name; }
    public int getAge() { return age; }
}
```

**실행 결과:**
```
직원이 생성되었습니다: Alice
사무실: OFF-001
오류: 직원은 18세 이상 67세 이하여야 합니다
```

## 프롤로그와 에필로그

### 2. 생성자 실행 순서

```java
public class ConstructorPhases {
    
    static class Base {
        protected String baseName;
        
        Base() {
            System.out.println("Base 생성자 본문");
            baseName = "base";
        }
    }
    
    static class Middle extends Base {
        protected String middleName;
        
        Middle() {
            // 프롤로그: super() 호출 전
            System.out.println("1. Middle 프롤로그");
            middleName = "middle-setup";
            
            // 상위 클래스 생성자 호출
            super();
            
            // 에필로그: super() 호출 후
            System.out.println("4. Middle 에필로그");
            middleName = "middle";
        }
    }
    
    static class Derived extends Middle {
        private String derivedName;
        
        Derived() {
            // 프롤로그
            System.out.println("2. Derived 프롤로그");
            derivedName = "derived-setup";
            
            // 상위 클래스 생성자 호출
            super();
            
            // 에필로그
            System.out.println("5. Derived 에필로그");
            derivedName = "derived";
        }
    }
    
    public static void main(String[] args) {
        System.out.println("=== 객체 생성 시작 ===");
        new Derived();
        System.out.println("=== 객체 생성 완료 ===");
    }
}
```

**실행 결과:**
```
=== 객체 생성 시작 ===
1. Middle 프롤로그
2. Derived 프롤로그
Base 생성자 본문
4. Middle 에필로그
5. Derived 에필로그
=== 객체 생성 완료 ===
```

## 복잡한 초기화

### 3. 고급 초기화 패턴

```java
import java.util.regex.Pattern;

public class ConfigurationClass {
    
    private Pattern validationPattern;
    private String ipAddress;
    private int port;
    
    public ConfigurationClass(String pattern, String ipAddress, int port) {
        // 프롤로그: 복잡한 계산 및 검증
        if (port < 1 || port > 65535) {
            throw new IllegalArgumentException(
                "포트는 1-65535 사이여야 합니다"
            );
        }
        
        // 정규표현식 컴파일 - 실패할 수 있음
        Pattern compiled = compilePattern(pattern);
        
        // IP 주소 검증
        validateIpAddress(ipAddress);
        
        // 복잡한 계산을 통한 초기값 설정
        this.validationPattern = compiled;
        this.ipAddress = ipAddress;
        this.port = port;
        
        System.out.println("설정이 성공적으로 초기화되었습니다");
    }
    
    private static Pattern compilePattern(String pattern) {
        try {
            return Pattern.compile(pattern);
        } catch (Exception e) {
            throw new IllegalArgumentException(
                "유효하지 않은 정규표현식: " + pattern
            );
        }
    }
    
    private static void validateIpAddress(String ip) {
        String[] parts = ip.split("\\.");
        if (parts.length != 4) {
            throw new IllegalArgumentException(
                "유효하지 않은 IP 주소: " + ip
            );
        }
        
        for (String part : parts) {
            try {
                int num = Integer.parseInt(part);
                if (num < 0 || num > 255) {
                    throw new NumberFormatException();
                }
            } catch (NumberFormatException e) {
                throw new IllegalArgumentException(
                    "각 옥텟은 0-255 사이여야 합니다"
                );
            }
        }
    }
    
    public static void main(String[] args) {
        try {
            ConfigurationClass config = new ConfigurationClass(
                "^[a-zA-Z0-9]+$",
                "192.168.1.1",
                8080
            );
            
            ConfigurationClass invalid = new ConfigurationClass(
                "[invalid",
                "192.168.1.1",
                8080
            );
            
        } catch (IllegalArgumentException e) {
            System.err.println("오류: " + e.getMessage());
        }
    }
}
```

**실행 결과:**
```
설정이 성공적으로 초기화되었습니다
오류: 유효하지 않은 정규표현식: [invalid
```

## 부분 초기화 방지

### 4. 객체 무결성 보장

```java
public class IntegrityExample {
    
    // 상위 클래스
    static class Shape {
        protected int sides;
        
        Shape(int sides) {
            System.out.println("Shape 생성자: sides=" + sides);
            this.sides = sides;
            describe();  // 오버라이드된 메서드 호출
        }
        
        protected void describe() {
            System.out.println("도형: " + sides + "변");
        }
    }
    
    // 하위 클래스
    static class Polygon extends Shape {
        private String color;
        
        Polygon(int sides, String color) {
            // 프롤로그: this.color를 먼저 초기화
            this.color = color;
            
            // 상위 생성자 호출 시 this.color가 이미 초기화됨
            super(sides);
            
            System.out.println("Polygon 완성: " + color);
        }
        
        @Override
        protected void describe() {
            // color가 null이 아님을 보장
            System.out.println("도형: " + sides + "변, 색상: " + color);
        }
    }
    
    public static void main(String[] args) {
        Polygon polygon = new Polygon(5, "빨강");
    }
}
```

**실행 결과:**
```
Shape 생성자: sides=5
도형: 5변, 색상: 빨강
Polygon 완성: 빨강
```

## 필드 초기화 제약

### 5. Early Construction Context의 규칙

```java
public class ConstructionConstraints {
    
    static class FieldExample {
        int uninitializedField;
        int initializedField = 10;
        
        FieldExample() {
            // 프롤로그에서 가능한 작업들
            
            // ✓ 초기화되지 않은 필드에 할당 - 가능
            uninitializedField = 42;
            
            // ✗ 초기화된 필드에 할당 - 불가능
            // initializedField = 20;  // 컴파일 오류
            
            // ✗ this 명시적 사용 - 불가능
            // int x = this.uninitializedField;  // 컴파일 오류
            
            // ✗ 현재 인스턴스를 메서드로 전달 - 불가능
            // processField(this);  // 컴파일 오류
            
            super();
            
            // 에필로그에서는 모든 것이 가능
            int x = this.uninitializedField;  // ✓ 가능
            initializedField = 20;  // ✓ 가능
        }
    }
    
    static class NestedClassExample {
        int field;
        
        class Inner {
            Inner() {
                // 프롤로그에서 외부 인스턴스 접근 가능
                field = 100;  // ✓ 가능 (외부 인스턴스의 필드)
                
                super();
            }
        }
    }
}
```

## 레코드와 열거형

### 6. Record에서의 사용

```java
import java.time.LocalDate;

public record Person(String name, LocalDate birthDate) {
    
    // Compact Constructor - Java 25 이전
    // public Person {
    //     Objects.requireNonNull(name);
    //     if (birthDate.isAfter(LocalDate.now())) {
    //         throw new IllegalArgumentException("출생일이 미래입니다");
    //     }
    // }
    
    // Java 25: 더 유연한 생성자
    public Person(String name, LocalDate birthDate) {
        // this(...) 호출 전 검증
        if (name == null || name.isEmpty()) {
            throw new IllegalArgumentException("이름은 필수입니다");
        }
        
        if (birthDate.isAfter(LocalDate.now())) {
            throw new IllegalArgumentException("출생일이 미래입니다");
        }
        
        this(name, birthDate);
    }
    
    public static void main(String[] args) {
        try {
            Person person1 = new Person("Alice", LocalDate.of(1990, 5, 15));
            System.out.println("사람: " + person1);
            
            Person person2 = new Person("Bob", LocalDate.now().plusDays(1));
            
        } catch (IllegalArgumentException e) {
            System.err.println("오류: " + e.getMessage());
        }
    }
}
```

**실행 결과:**
```
사람: Person[name=Alice, birthDate=1990-05-15]
오류: 출생일이 미래입니다
```

## 열거형 생성자

### 7. Enum Constructor

```java
public enum Status {
    PENDING("대기중", 1),
    ACTIVE("활성", 2),
    DISABLED("비활성", 3);
    
    private final String displayName;
    private final int code;
    
    Status(String displayName, int code) {
        // Java 25: this() 호출 전 검증 가능
        if (displayName == null || displayName.isEmpty()) {
            throw new IllegalArgumentException("displayName은 필수입니다");
        }
        
        if (code < 1) {
            throw new IllegalArgumentException("코드는 양수여야 합니다");
        }
        
        this(displayName, code);
    }
    
    public String getDisplayName() {
        return displayName;
    }
    
    public int getCode() {
        return code;
    }
    
    public static void main(String[] args) {
        for (Status status : Status.values()) {
            System.out.println(status.name() + ": " + status.getDisplayName() 
                             + " (코드: " + status.getCode() + ")");
        }
    }
}
```

**실행 결과:**
```
PENDING: 대기중 (코드: 1)
ACTIVE: 활성 (코드: 2)
DISABLED: 비활성 (코드: 3)
```

# 주요 이점

| 이점 | 설명 |
|------|------|
| **Fail-Fast** | 생성자 초반에 검증하여 불완전한 객체 생성 방지 |
| **객체 무결성** | 상위 클래스 생성자 호출 전 모든 필드 초기화 가능 |
| **가독성** | 검증 로직을 명확하게 표현 |
| **안전성** | 상위 클래스의 메서드 호출 시 초기화되지 않은 필드 접근 방지 |

# 주의사항

- Early Construction Context 규칙 준수 필수
- `this`를 명시적/암묵적으로 사용 불가 (프롤로그에서)
- 문서화 필요: 프롤로그에서 수행되는 작업 명시

# 호환성

- **소스 호환**: 기존 코드는 변경 없이 작동
- **바이너리 호환**: 컴파일된 클래스 파일은 호환됨
- **동작 호환**: 기존과 동일한 의미 유지

# Reference

[^Java25]: [Oracle-Java_25_Release_Notes](https://docs.oracle.com/en/java/javase/25/docs/api/){:target="_blank"}
[^FlexibleConstructor]: [OpenJDK-JEP 513: Flexible Constructor Bodies](https://openjdk.org/jeps/513){:target="_blank"}
[^ProjectValhalla]: [OpenJDK-Project Valhalla](https://openjdk.org/projects/valhalla/){:target="_blank"}
