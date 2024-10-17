---
title: "Leetcode Java Fraction to Recurring Decimal"
excerpt: "Leetcode - 'Fraction to Recurring Decimal' 문제 Java 풀이"
last_modified_at: 2021-09-17T12:00:00
header:
  image: /assets/images/leetcode/fraction-to-recurring-decimal.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/fraction-to-recurring-decimal/){:target="_blank"}

# 코드
```java
class Solution {

  public String fractionToDecimal(int numerator, int denominator) {
    StringBuilder result = new StringBuilder();
    if ((numerator > 0 && denominator < 0) || (numerator < 0 && denominator > 0)) {
      result.append("-");
    }
    long numeratorLong = Math.abs((long) numerator);
    long denominatorLong = Math.abs((long) denominator);
    result.append(numeratorLong / denominatorLong);
    long remainder = numeratorLong % denominatorLong;
    if (remainder == 0) {
      return result.toString();
    }
    result.append(".");
    Map<Long, Integer> map = new HashMap<>();
    while (remainder != 0) {
      if (!map.containsKey(remainder)) {
        map.put(remainder, result.length());
      } else {
        result.insert(map.get(remainder), "(");
        result.append(")");
        return result.toString();
      }
      remainder *= 10;
      result.append(remainder / denominatorLong);
      remainder %= denominatorLong;
    }
    return result.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/556170526/){:target="_blank"}

# 설명
1. 주어진 분수 표기법의 변수들인 numerator(분자)와 denominator(분모)를 이용하여 소수 표기법으로 변환하는 문제이다.
- 단, [순환소수](https://ko.wikipedia.org/wiki/%EC%88%9C%ED%99%98%EC%86%8C%EC%88%98){:target="_blank"}인 경우 순환마디를 소괄호()로 감싸 표기한다.

2. 결과를 동적으로 생성하기 위해 StringBuilder인 result를 정의한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

3. 주어진 분자인 numerator와 분모인 denominator의 곱이 음의 정수(-)가 되는 경우는 초기 값에 "-" 기호를 넣어준다.

4. 주어진 분자인 numerator와 분모인 denominator을 양의 정수인 long 형태로 각각 변경하여 numeratorLong과 denominatorLong을 정의한다.

5. result에 $\frac{numeratorLong}{denominatorLong}$의 정수 값을 넣어주고, 나머지 값은 remainder 변수를 정의하여 넣어준다.
- remainder가 0일 경우 나눗셈의 결과가 정수가 되는 경우이므로, result를 문자형으로 전환하여 주어진 문제의 결과로 반환한다.

6. result에 소수점(.)을 추가하고, 순환마디를 구하기 위해 map을 정의하고 remainder가 0이 아닐 때 까지 반복하여 result를 완성한다.
- map에 remainder가 key로 존재하지 않은 경우, 아래를 수행한다.
  - key는 remainder, value는 순환마디의 시작 위치인 result의 길이로 넣어준다.
  - remainder에 10을 곱하여 result에 $\frac{remainder}{dominatorLong}$의 정수 값을 넣어주고,
  remainder에는 나머지 값을 넣어주고 반복을 계속 수행한다.
- map에 remainder가 key로 존재하는 경우, 아래를 수행한다.
  - map에서 해당 remainder 값인 순환마디의 시작 위치를 가져와 해당 위치에 "(" 문자를 넣어주고, result에 ")"문자를 넣어 순환 마디를 소괄호()로 감싸준다.
  - 순환소수가 저장된 result를 문자형으로 전환하여 주어진 문제의 결과로 반환한다.

7. 반복이 완료되면 순환소수가 아닌 result를 문자형으로 전환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FractionToRecurringDecimal.java){:target="_blank"}에서 확인 가능합니다.