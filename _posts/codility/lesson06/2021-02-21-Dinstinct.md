---
title: "Codility Distinct"
excerpt: "Lesson6. Sorting"
last_modified_at: 2021-02-21T12:13:00
header:
  image: /assets/images/codility/lesson06/Distinct.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Sorting

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/6-sorting/distinct/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    return (int) Arrays.stream(A).distinct().count();
  }
}
```

# 설명
1. 주어진 배열 A의 중복을 제거한 숫자를 반환하면 된다.

# 결과
[Link](https://app.codility.com/demo/results/trainingBUTFHG-DS3/)

# 소스
[GitHub-Distinct](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson06/Distinct.java)