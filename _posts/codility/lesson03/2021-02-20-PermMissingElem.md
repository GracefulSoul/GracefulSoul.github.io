---
title: "Codility Java PermMissingElem"
excerpt: "Lesson3. Time Complexity"
last_modified_at: 2021-02-20T15:19:00
header:
  image: /assets/images/codility/lesson03/PermMissingElem.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Time Complexity
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/3-time_complexity/perm_missing_elem/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int difference = A.length + 1;
    for (int idx = 0; idx < A.length; idx++) {
      difference += (idx + 1) - A[idx];
    }
    return difference;
  }
}
```

# 설명
1. 배열 A 내 값이 최소 값은 1이고 최대 값은 배열 N의 크기 + 1이므로, Index + 1의 합과 배열 A의 값의 합을 빼면 빠진 값이 도출된다.

# 결과
[Link](https://app.codility.com/demo/results/trainingMBK8M8-JET/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson03/PermMissingElem.java){:target="_blank"}에서 확인 가능합니다.