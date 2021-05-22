---
title: "Codility Java MaxProfit"
excerpt: "Lesson9. Maximum Slice Problem"
last_modified_at: 2021-02-28T13:47:00
header:
  image: /assets/images/codility/lesson09/MaxProfit.png
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
[Link](https://app.codility.com/programmers/lessons/9-maximum_slice_problem/max_profit/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int result = 0;
    // The function should return 0 if it was impossible to gain any profit.
    if (A.length < 2) {
      return 0;
    }
    int min = A[0];
    for (int idx = 1; idx < A.length; idx++) {
      if (A[idx] < min) {
        min = A[idx];
      } else {
        int temp = A[idx] - min;
        if (result < temp) {
          result = temp;
        }
      }
    }
    return result;
  }
}
```

# 설명
1. 주어진 배열 A의 크기가 2보다 작으면 이익을 계산할 수 없으므로, 0을 주어진 문제의 결과로 반환한다.
2. 초기 최소값을 주어진 배열 A의 0번째 인덱스로 초기화 하고, 최대 이익을 계산한다.
- 최대 이익은 현재 값과 최소 값의 차이가 가장 큰 지점을 찾아야 하므로, 만일 최소값을 저장한 변수 min보다 작은 값이 주어진 경우 min에 현재 값을 저장한다.
- 위의 경우가 아니면 현재 값을 최소값을 저장한 변수 min의 차이를 결과로 임시 저장을 한다.
3. 반복이 끝나면 최대 이익을 계산한 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingTQDNU5-K6T/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson09/MaxProfit.java){:target="_blank"}에서 확인 가능합니다.