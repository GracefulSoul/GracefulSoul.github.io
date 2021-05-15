---
title: "MyBatis java.lang.NoSuchMethodException: java.lang.Long.<init>() 원인과 해결"
excerpt: "MyBatis Cause: org.apache.ibatis.reflection.ReflectionException: Error instantiating class java.lang.Long with invalid types () or values (). Cause: java.lang.NoSuchMethodException: java.lang.Long.<init>()"
last_modified_at: 2021-05-13T13:00:00
header:
  image: /assets/images/java/mybatis-nosuchmethodexception.png
categories:
  - Java
tags:
  - Programming
  - Java
  - MyBatis

toc: true
toc_ads: true
toc_sticky: true
---
# 오류 발생
- Mapper

```xml
  <!-- ... -->
  <select id="getCustomer" parameterType="java.lang.Long">
    SELECT * FROM customer
    WHERE id = #{id}
  </select>
  <!-- ... -->
```

- 간단히 주어진 고객 id를 이용하여, 해당 고객의 정보를 가져오는 쿼리를 Mapper에 생성하였다.

- Console Log

```text
org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database.  Cause: org.apache.ibatis.reflection.ReflectionException: Error instantiating class java.lang.Long with invalid types () or values (). Cause: java.lang.NoSuchMethodException: java.lang.Long.<init>()
### The error may exist in gracefulsoul/mybatis/resouces/mapper/CustomerMapper.xml
### The error may involve gracefulsoul.mybatis.resouces.mapper.CustomerMapper.getCustomer
### The error occurred while handling results
### SQL: SELECT * FROM customer     WHERE id = ?
### Cause: org.apache.ibatis.reflection.ReflectionException: Error instantiating class java.lang.Long with invalid types () or values (). Cause: java.lang.NoSuchMethodException: java.lang.Long.<init>()
```

- 해당 쿼리를 수행하는 API를 호출하게 되면 갑자기 이런 오류가 발생한다.
- 오류 내용을 확인하면 MyBatis에서 Reflection을 사용하는데, java.lang.Long 클래스의 Default Constructor(기본 생성자)가 존재하지 않는다고 오류가 발생하였다.

# 원인 분석
- Java Docs - java.lang.Long

```java
  /* line 932 */
  /**
    * The value of the {@code Long}.
    *
    * @serial
    */
  private final long value;

  /**
    * Constructs a newly allocated {@code Long} object that
    * represents the specified {@code long} argument.
    *
    * @param   value   the value to be represented by the
    *          {@code Long} object.
    */
  public Long(long value) {
      this.value = value;
  }

  /**
    * Constructs a newly allocated {@code Long} object that
    * represents the {@code long} value indicated by the
    * {@code String} parameter. The string is converted to a
    * {@code long} value in exactly the manner used by the
    * {@code parseLong} method for radix 10.
    *
    * @param      s   the {@code String} to be converted to a
    *             {@code Long}.
    * @throws     NumberFormatException  if the {@code String} does not
    *             contain a parsable {@code long}.
    * @see        java.lang.Long#parseLong(java.lang.String, int)
    */
  public Long(String s) throws NumberFormatException {
      this.value = parseLong(s, 10);
  }
  /* line 967 */
```

- 위의 Java Docs 내 java.lang.Long 소스코드를 보면 Default Constructor가 존재하지 않는 것을 확인 할 수 있다.
- MyBatis에서는 Reflection을 이용하여 동적인 파라미터 초기화를 수행하므로, 기본 생성자가 없으면 객체 초기화가 불가능하기 때문에 당연히 오류가 발생하게 된다.
- 그렇기 때문에 MyBatis에서 java.lang.Long을 parameterType으로 명시할 경우, 해당 타입의 기본 생성자가 없으므로 오류가 발생한다.

# 오류 해결
- Mapper

```xml
  <!-- ... -->
  <select id="getCustomer">
    SELECT * FROM customer
    WHERE id = #{id}
  </select>
  <!-- ... -->
```

- 해결 방법은 Mapper 내 getCustomer에 parameterType을 명시하지 않도록 처리하였다.
- 이렇게 실제 주입한 파라미터가 java.lang.Long이어도 오류가 발생하지 않는 이유는 AutoBoxing과 Unboxing에 의해 타입 유추가 되어 위의 Exception이 발생하지 않는 것이다.