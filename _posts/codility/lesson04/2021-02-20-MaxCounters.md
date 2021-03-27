---
title: "Codility Java MaxCounters"
excerpt: "Lesson4. Counting Elements"
last_modified_at: 2021-02-20T15:50:00
header:
  image: /assets/images/codility/lesson04/MaxCounters.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Counting Elements
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int[] solution(int N, int[] A) {
    int[] result = new int[N];
    int max = 0;
    int init = 0;
    for (int num : A) {
      if (num == N + 1) { // Over than array size and maximum number is N + 1.
        // Set init value using max value.
        init = max;
      } else {
        if (init > result[num - 1]) {
          result[num - 1] = init + 1;
        } else {
          result[num - 1]++;
        }
        // Save maximum value.
        if (result[num - 1] > max) {
          max = result[num - 1];
        }
      }
    }
    // If lower than init value, change each values.
    for (int idx = 0; idx < N; idx++) {
      if (result[idx] < init) {
        result[idx] = init;
      }
    }
    return result;
  }
}
```

# 설명
1. 주어진 크기 N의 배열 result를 생성한다.
2. 주어진 배열인 A를 반복하여 해당 값에 위치한 배열 result의 값을 더한다.
- 만일 주어진 배열의 크기보다 큰 index가 나오는지를 확인해서 init 변수에 max 값를 넣는다.
- 주어진 배열의 크기보다 낮은 경우 result의 해당 index 값이 init 보다 작은지를 확인하여, 작으면 init + 1로 값을 초기화 한다.
3. 더해진 값의 크기가 max보다 크다면 배열보다 큰 값인 N + 1이 나올 때 초기값을 설정하기 위해 max에 최대 값을 저장한다.
4. 마지막으로 결과로 반환할 배열 result의 값이 init보다 작다면, init 값으로 초기화 하고 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingQ5G9KP-C39/)

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson04/MaxCounters.java)에서 확인 가능합니다.