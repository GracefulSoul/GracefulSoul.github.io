---
title: "Codility MinAvgTwoSlice"
excerpt: "Lesson5. Prefix Sums"
last_modified_at: 2021-02-21T11:44:00
header:
  image: /assets/images/codility/lesson05/MinAvgTwoSlice.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Prefix Sums

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/5-prefix_sums/min_avg_two_slice/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int result = 0;
    double minimumAverage = (A[0] + A[1]) / 2.0d;
    for (int idx = 2; idx < A.length; idx++) {
      double average = (A[idx - 2] + A[idx - 1] + A[idx]) / 3.0d;
      if (minimumAverage > average) {
        minimumAverage = average;
        result = idx - 2;
      }
      average = (A[idx - 1] + A[idx]) / 2.0d;
      if (minimumAverage > average) {
        minimumAverage = average;
        result = idx - 1;
      }
    }
    return result;
  }
}
```

# 설명
1. 초기 평균 최소값은 주어진 배열 A의 0번째와 1번째 값의 평균으로 저장한다.
- 단, 배열 A의 값들은 정수형이므로 실수형으로 변환하여야 한다.
2. index는 2부터 시작하여 반복문을 통해 평균이 최소가 되는 지점을 탐색한다.
- index가 2부터 시작하는 이유는 평균이 최소가 되는 부분의 탐색의 범위를 3까지 하기 때문이다.
- 탐색의 범위가 3까지인 이유는 범위가 4 이후의 평균은 범위가 2, 3의 평균에 비해 같거나 높아지기 때문에 제외한다.
3. 범위가 2, 3인 경우의 평균이 초기 평균 최소값보다 작다면 해당 값과 시작 index를 저장한다.
4. 반복이 완료되면 최소 평균이 나오는 시작점을 저장한 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/training8NYBNN-9FU/)

# 소스
[GitHub-MinAvgTwoSlice](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson05/MinAvgTwoSlice.java)