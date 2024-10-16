---
title: "Codility Java MaxDoubleSliceSum"
excerpt: "Lesson9. Maximum Slice Problem"
last_modified_at: 2021-02-28T13:20:00
header:
  image: /assets/images/codility/lesson09/MaxDoubleSliceSum.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Maximum Slice Problem
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/9-maximum_slice_problem/max_double_slice_sum/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int result = 0;
    // Init subsum arrays.
    int[] firstSubSum = new int[A.length];
    for (int idx = 1; idx < A.length - 1; idx++) {
      firstSubSum[idx] = Math.max(0, firstSubSum[idx - 1] + A[idx]);
    }
    int[] secondSubSum = new int[A.length];
    for (int idx = A.length - 2; idx >= 1; idx--) {
      secondSubSum[idx] = Math.max(0, secondSubSum[idx + 1] + A[idx]);
    }
    // Calculate max(result) value.
    for (int idx = 1; idx < A.length - 1; idx++) {
      int temp = firstSubSum[idx - 1] + secondSubSum[idx + 1];
      if (temp > result) {
        result = temp;
      }
    }
    return result;
  }
}
```

# 설명
1. 세 인덱스 사잇 값들을 더한 값을 보관하기 2개의 배열 firstSubSum, secondSubSum을 생성하여 반복문을 통해 계산한다.
- 반복의 초기 값은 배열의 처음과 마지막 값을 빼고 계산해야 하기 때문에 0과 A.length - 1의 값은 제외한다.
- firstSubSum 계산은 정방향으로, secondSubSum 계산은 역방향으로 누적합계를 구한다.
2. 특정 인덱스가 주어지면, 해당 인덱스 기준으로 사잇 값의 누계를 합하여 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingZ9SZBR-5H4/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson09/MaxDoubleSliceSum.java){:target="_blank"}에서 확인 가능합니다.