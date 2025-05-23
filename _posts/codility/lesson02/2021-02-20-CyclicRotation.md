---
title: "Codility Java CyclicRotation"
excerpt: "Lesson2. Arrays"
last_modified_at: 2021-02-20T14:16:00
header:
  image: /assets/images/codility/lesson02/CyclicRotation.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Arrays
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/2-arrays/cyclic_rotation/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int[] solution(int[] A, int K) {
    int length = A.length;
    int[] result = new int[length];
    // Repeat the size of array A.
    for (int idx = 0; idx < length; idx++) {
      result[(idx + K) % length] = A[idx];
    }
    return result;
  }
}
```

# 설명
1. 결과를 반환할 새로운 int array를 생성한다.
- 순서만 변경되므로, 배열의 사이즈는 매개변수 A와 같다.
2. 배열을 반복하면서 배열 result에 배열 A의 값을 넣어준다.
- 기존 index의 값에 반복횟수인 K를 더해서 이동시키고, 배열의 크기를 벗어나면 0번째 index로 이동하여 계산하여야 한다.
- 위의 조건을 계산식으로 변환하면 A의 idx번째 들어있는 값은 result의 (idx + K) % length번째 index에 들어가야 한다.
3. 주어진 문제의 결과를 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingUWMRMK-AWK/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson02/CyclicRotation.java){:target="_blank"}에서 확인 가능합니다.