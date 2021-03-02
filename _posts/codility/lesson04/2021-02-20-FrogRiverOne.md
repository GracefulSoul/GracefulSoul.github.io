---
title: "Codility FrogRiverOne"
excerpt: "Lesson4. Counting Elements"
last_modified_at: 2021-02-20T15:03:00
header:
  image: /assets/images/codility/lesson04/FrogRiverOne.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Counting Elements

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/4-counting_elements/frog_river_one/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

import java.util.Set;
import java.util.HashSet;

class Solution {
  public int solution(int X, int[] A) {
    Set<Integer> leafs = new HashSet<>();
    for (int idx = 0; idx < A.length; idx++) {
      leafs.add(A[idx]);
      // Get to the goal.
      if (X == leafs.size()) {
        return idx;
      }
    }
    return -1;
  }
}
```

# 설명
1. 목표 지점에 도달하기 까지 잎의 위치를 저장할 Collection을 사용한다.
- 중복된 잎의 위치는 의미가 없으므로 유일 값을 저장할 수 있는 Set을 사용한다.
2. 잎의 위치를 가지고 있는 배열 A를 반복하여 leafs에 넣는다.
3. 만약 목표 지점과 leafs의 크기가 동일하면 현재 index를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingJ8UD3S-3CE/)

# 소스
[GitHub-FrogRiverOne](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson04/FrogRiverOne.java)