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
  - Counting Elements

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

import java.util.Arrays;

class Solution {
  public int solution(int[] A) {
    Arrays.sort(A);
    for (int idx = 0; idx < A.length; idx++) {
      if (A[idx] != idx + 1) {
        return 0;
      }
    }
    return 1;
  }
}
```

# 설명
1. 순서대로 숫자가 들어있는지 확인하기 위해서 배열을 정렬한다.
2. 배열 A를 반복하여 A의 idx번째 있는 값이 idx + 1이 아니면 0을 주어진 문제의 결과로 반환한다.
3. for문이 정상적으로 실행 되었을 경우, 배열의 크기만큼의 연속된 숫자가 들어있으므로 1을 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingJZTBZU-BE7/)

# 소스
[GitHub-PermCheck](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson04/PermCheck.java)