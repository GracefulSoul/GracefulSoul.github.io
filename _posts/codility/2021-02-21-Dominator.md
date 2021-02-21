---
title: "Codility Dominator"
excerpt: "Lesson8. Leader"
last_modified_at: 2021-02-21T15:04:00
header:
  image: /assets/images/codility/Dominator.png
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
[Link](https://app.codility.com/programmers/lessons/8-leader/dominator/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

import java.util.Map;
import java.util.HashMap;

class Solution {
  public int solution(int[] A) {
    Map<Integer, Integer> map = new HashMap<>();
    // Calculate how many numbers are in the array(A).
    for (int num : A) {
      map.put(num, map.getOrDefault(num, 0) + 1);
    }
    int num = 0;
    int max = 0;
    for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
      if (entry.getValue() > max) {
        num = entry.getKey();
        max = entry.getValue();
      }
    }
    // If not half of array(A)'s size, return -1.
    if (max <= A.length / 2) {
      return -1;
    }
    // Find index of num.
    for (int idx = 0; idx < A.length; idx++) {
      if (A[idx] == num) {
        return idx;
      }
    }
    return -1;
  }
}
```

# 설명
1. 주어진 배열 A에 들어간 숫자가 몇 번 반복되었는지를 계산하기 위해 Map을 사용한다.
2. 주어진 배열 A를 반복하여 변수 map에 숫자를 key로 반복 횟수를 value로 증가시켜준다.
3. 변수 map에서 가장 많이 반복된 숫자와 갯수를 가져온다.
4. 만일 주어진 배열 A 크기의 절반보다 작은 경우 -1을 주어진 문제의 결과로 반환한다.
5. 주어진 배열 A에서 가장 많이 반복된 숫자의 index를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingBN5US6-ESY/)

# 소스
[GitHub-Dominator](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson08/Dominator.java)