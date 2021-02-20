---
title: "Codility PermCheck"
excerpt: "Lesson4. Counting Elements"
last_modified_at: 2021-02-20T16:26:00
header:
  image: /assets/images/codility/PermCheck.png
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
[Link](https://app.codility.com/programmers/lessons/4-counting_elements/perm_check/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

import java.util.Set;
import java.util.HashSet;

class Solution {
  public int solution(int[] A) {
    Set<Integer> numSet = new HashSet<>();
    for (int num : A) {
      if (num > A.length || numSet.contains(num)) { // If over than array's size or duplicated number.
        return 0;
      } else {
        numSet.add(num);
      }
    }
    return 1;
  }
}
```

# 설명
1. 중복된 숫자를 제거하기 위해 Set을 사용하여 numSet을 정의한다.
2. 배열 A를 반복하여 배열의 크기보다 크거나 중복된 숫자가 없을 경우 numSet에 추가하고, 있을 경우 0을 주어진 문제의 결과로 반환한다.
3. for문이 정상적으로 실행 되었을 경우, 배열의 크기만큼 연속된 숫자가 들어있으므로 1을 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingDCMXJY-HDN/)

# 소스
[GitHub-PermCheck](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson04/PermCheck.java)