---
title: "Codility Java MaxProductOfThree"
excerpt: "Lesson6. Sorting"
last_modified_at: 2021-02-21T12:30:00
header:
  image: /assets/images/codility/lesson06/MaxProductOfThree.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Sorting
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/6-sorting/max_product_of_three/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    Arrays.sort(A);
    // The initial value is set to a value greater than 3.
    int result = A[A.length - 3] * A[A.length - 2] * A[A.length - 1];
    // Check if the two smallest values are negative and the largest value is positive.
    if (A[0] < 0 && A[1] < 0 && A[A.length - 1] > 0) {
      int temp = A[0] * A[1] * A[A.length - 1];
      if (result < temp) {
        result = temp;
      }
    }
    return result;
  }
}
```

# 설명
1. 주어진 배열 A를 Arrays 클래스를 활용하여 오름차순 정렬한다.
2. 기본 최대값은 정렬된 배열 A의 최대 3개의 값으로 한다.
3. 만일, 가장 낮은 두 값이 음수이고 가장 큰 값이 양수인 경우에는 최대값을 저장한 result와 비교하여 최대값을 다시 설정한다.
4. 최대값을 저장한 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/training6ZYATQ-GE7/)

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/lesson06/MaxProductOfThree.java)에서 확인 가능합니다.