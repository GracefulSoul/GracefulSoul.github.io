---
title: "Codility Java MaxSliceSum"
excerpt: "Lesson9. Maximum Slice Problem"
last_modified_at: 2021-02-28T14:07:00
header:
  image: /assets/images/codility/lesson09/MaxSliceSum.png
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
[Link](https://app.codility.com/programmers/lessons/9-maximum_slice_problem/max_slice_sum/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int result = A[0];
    int sum = A[0];
    for (int idx = 1; idx < A.length; idx++) {
      sum = Math.max(A[idx], sum + A[idx]);
      if (result < sum) {
        result = sum;
      }
    }
    return result;
  }
}
```

# 설명
1. 최소 배열의 크기가 1개이므로, 결과를 저장하는 result는 주어진 배열 A의 0번째 인덱스의 값으로 초기화 한다.
2. 1번의 이유로 반복은 1번째 인덱스부터 반복을 돌려 최대 값을 탐색한다.
  - 해당 값이 이전의 최대 합보다 크다면, 해당 값부터 합계가 시작하도록 최대 합계를 저장하는 변수 sum에 저장한다.
  - 만일 최대 합계를 저장하는 변수 sum이 결과를 저장하는 변수 result보다 크다면 result에 최대 합계로 저장한다.
3. 반복이 끝나면 최대 합계를 저장한 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingNXT2S3-3U7/)

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson09/MaxSliceSum.java)에서 확인 가능합니다.