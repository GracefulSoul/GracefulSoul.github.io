---
title: "Leetcode Java Integer to Roman"
excerpt: "Leetcode Integer to Roman Java 풀이"
last_modified_at: 2021-04-20T18:10:00
header:
  image: /assets/images/leetcode/integer-to-roman.png
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
[Link](https://leetcode.com/problems/integer-to-roman/){:target="_blank"}

# 코드
```java
class Solution {

  public String intToRoman(int num) {
    String[] romans = new String[] { "M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I" };
    int[] nums = new int[] { 1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1 };
    StringBuilder sb = new StringBuilder();
    int idx = 0;
    while (num > 0) {
      int multiple = num / nums[idx];
      for (int i = 0; i < multiple; i++) {
        num -= nums[idx];
        sb.append(romans[idx]);
      }
      idx++;
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/482958970/){:target="_blank"}

# 설명
1. 정수 숫자와 로마 숫자를 각 배열 nums와 romans에 정의한다.
  - 같은 index에 해당 값이 존재하므로 1:1 매칭이 되어, 다른 배열로 정의하여도 된다.
  - 높은 순서대로 정의하여, 순차 계산할 경우 오름차순으로 정렬된 로마 숫자 표현식이 되도록 한다.

2. 로마 숫자 표현식을 동적으로 만들기 위해 변수 sb를 선언한다.
  - 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

3. 로마 숫자 표현식의 순차 처리를 위해 변수 idx를 0으로 초기화하고, num이 0 이하가 될 때 까지 반복문을 수행하여 로마 숫자 표현식을 완성한다.
  - 주어진 정수 num을 idx번째 nums 배열의 숫자를 나눈 몫만큼 반복하여 변수 sb에 idx번째 roman 배열의 문자열을 반복하고, 주어진 정수 num을 idx번째 숫자를 빼준다.
  - 위의 반복이 완료되면 idx를 증가시켜 다음 로마 숫자를 이용하여 로마 숫자 표현식을 완성한다.

4. 3번의 반복이 완료되면 변수 sb를 String으로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IntegerToRoman.java){:target="_blank"}에서 확인 가능합니다.