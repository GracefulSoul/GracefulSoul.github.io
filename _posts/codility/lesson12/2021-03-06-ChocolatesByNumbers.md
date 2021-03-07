---
title: "Codility ChocolatesByNumbers"
excerpt: "Lesson11. Euclidean algorithm"
last_modified_at: 2021-03-07T13:27:00
header:
  image: /assets/images/codility/lesson11/ChocolatesByNumbers.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Euclidean algorithm

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/12-euclidean_algorithm/chocolates_by_numbers/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int N, int M) {
    return N / getGcd(M, N);
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
1. 유클리드 호제법[^Euclidean]을 사용하여 1에서 부터 주어진 정수 N까지 M을 이용해서 최대 공약수를 먼저 구한다.
2. 주어진 정수 N을 유클리드 호제법을 통해 구한 최대 공약수로 나누어서 나온 먹을 초콜릿의 갯수를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/training2XBK6X-U2F/)

# 소스
[GitHub-ChocolatesByNumbers](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson12/ChocolatesByNumbers.java)

# Reference
[^Euclidean]: [Wiki-Euclidean_Algorithm](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95)