---
title: "Codility TapeEquilibrium"
excerpt: "Lesson3. Time Complexity"
last_modified_at: 2021-02-20T15:03:00
header:
  image: /assets/images/codility/TapeEquilibrium.png
categories:
  - Codility
tags:
  - Programming
  - Codility

toc: true
toc_ads: true
toc_sticky: true
---

# 문제
[Link](https://app.codility.com/programmers/lessons/3-time_complexity/tape_equilibrium/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int min = Integer.MAX_VALUE;
    int sum = sum(A);
    int subSum = 0;
    for (int idx = 0; idx < A.length - 1; idx++) {
      subSum += A[idx];
      sum -= A[idx];
      int difference = Math.abs(subSum - sum);
      if (difference < min) {
        min = difference;
      }
    }
    return min;
  }
  private int sum(int[] A) {
    int sum = 0;
    for (int num : A) {
      sum += num;
    }
    return sum;
  }
}
```

# 설명
1. 특정 index 기준으로 우측 합을 더하는 sum과 좌측 합을 더하는 subSum을 정의한다.
2. 반복을 하면서 좌측 합과 우측 합의 차이를 구한다.
- 최소 값이 위의 차이보다 클 경우에, 차이 값을 최소 값으로 넣어준다.
3. 주어진 문제의 결과를 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/training2C4RED-4GW/)

# 소스
[GitHub-TapeEquilibrium](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson03/TapeEquilibrium.java)