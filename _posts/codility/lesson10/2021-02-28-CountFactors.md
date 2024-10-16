---
title: "Codility Java CountFactors"
excerpt: "Lesson10. Prime And Composite Numbers"
last_modified_at: 2021-02-28T14:41:00
header:
  image: /assets/images/codility/lesson10/CountFactors.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Prime And Composite Numbers
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/10-prime_and_composite_numbers/count_factors/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int N) {
    if (N == 1) {
      return N;
    }
    int result = 1;
    for (int idx = 2; idx < Math.sqrt(N); idx++) {
      if (N % idx == 0) {
        result++;
      }
    }
    result = result * 2;
    if (Math.sqrt(N) % 1 == 0) {
      result++;
    }
    return result;
  }
}
```

# 설명
1. 주어진 변수 N이 1일 경우 1개이므로, 그대로 주어진 문제의 결과로 반환한다.
2. 결과값을 담는 변수 result는 1인 경우를 포함하여 1로 초기화 한다.
3. 2번의 이유로 2부터 주어진 변수 N의 제곱근의 값만큼 반복한다.
- 주어진 변수 N이 만일 정수라면, N의 제곱근의 인수는 해당 값을 전후로 개수가 동일하게 된다.
4. 3번의 이유로 반복이 끝나면 인수의 개수를 담은 result에 2를 곱하고, 만일 제곱근의 값이 정수라면 1을 더해서 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingWRXP78-3U7/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson10/CountFactors.java){:target="_blank"}에서 확인 가능합니다.