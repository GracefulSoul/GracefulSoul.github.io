---
title: "Codility Java MissingInteger"
excerpt: "Lesson4. Counting Elements"
last_modified_at: 2021-02-20T16:12:00
header:
  image: /assets/images/codility/lesson04/MissingInteger.png
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
[Link](https://app.codility.com/programmers/lessons/4-counting_elements/missing_integer/){:target="_blank"}

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
      if (num > 0) { // Greater than 0.
        numSet.add(num);
      }
    }
    for (int idx = 1; idx <= Integer.MAX_VALUE; idx++) {
      if (!numSet.contains(idx)) {
        return idx;
      }
    }
    return 1;
  }
}
```

# 설명
1. 누락된 숫자를 파악하기 위해 중복을 제거한 Set을 사용하여 numSet을 정의한다.
2. 배열 A를 반복하여 양수만 numSet에 추가한다.
3. 1부터 1씩 증가하며 numSet에 포함되어있는지 확인하고, 없을 경우 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/training6RJEX8-PHQ/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson04/MissingInteger.java){:target="_blank"}에서 확인 가능합니다.