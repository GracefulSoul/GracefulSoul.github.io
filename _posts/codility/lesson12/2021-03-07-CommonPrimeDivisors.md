---
title: "Codility Java CommonPrimeDivisors"
excerpt: "Lesson12. Euclidean Algorithm"
last_modified_at: 2021-03-07T13:27:00
header:
  image: /assets/images/codility/lesson12/CommonPrimeDivisors.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Euclidean Algorithm
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/12-euclidean_algorithm/common_prime_divisors/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A, int[] B) {
    int result = 0;
    for (int idx = 0; idx < A.length; idx++) {
      if (isSameDivisors(A[idx], B[idx])) {
        result++;
      }
    }
    return result;
  }
  // Check whether the sets of prime divisors of integers N and M are exactly the same.
  private boolean isSameDivisors(int num1, int num2) {
    int gcd = getGcd(num1, num2);
    return getDivisor(gcd, num1) == 1 && getDivisor(gcd, num2) == 1;
  }
  private int getDivisor(int gcd, int num) {
    int quotient = 0;
    while (quotient != 1) {
      quotient = getGcd(num, gcd);
      num /= quotient;
    }
    return num;
  }
  // Euclidean algorithm.
  private int getGcd(int num1, int num2) {
    if (num1 % num2 == 0) {
      return num2;
    } else {
      return getGcd(num2, num1 % num2);
    }
  }
}
```

# 설명
1. 유클리드 호제법[^Euclidean]을 사용하여 주어진 배열 A와 B 특정 idx에 속한 값의 최대 공약수를 구하여 변수 gcd로 임시 보관을 한다.
2. 구한 최대 공약수를 이용하여 배열 A와 B 특정 idx에 속한 값의 소인수가 각각 1인지를 확인하여 true면 소수 집합이 동일한 값의 갯수를 저장하는 변수 result를 증가 시키고, 그렇지 않으면 다음 idx에 속한 값으로 넘어간다.
3. 반복이 끝나면 소수 집합이 동일한 값의 갯수를 저장하는 변수 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingHCMKR3-3PJ/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson12/CommonPrimeDivisors.java){:target="_blank"}에서 확인 가능합니다.

# Reference
[^Euclidean]: [Wiki-Euclidean_Algorithm](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95){:target="_blank"}