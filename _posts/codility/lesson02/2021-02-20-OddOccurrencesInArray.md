---
title: "Codility Java OddOccurrencesInArray"
excerpt: "Lesson2. Arrays"
last_modified_at: 2021-02-20T14:33:00
header:
  image: /assets/images/codility/lesson02/OddOccurrencesInArray.png
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
[Link](https://app.codility.com/programmers/lessons/2-arrays/odd_occurrences_in_array/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int result = 0;
    for (int num : A) {
      // Using bit operation.
      result ^= num;
    }
    return result;
  }
}
```

# 설명
1. 배열 A를 반복하여 반복이 없는 숫자를 확인한다.
- 비트 연산의 배타적 논리합을 사용할 경우 같은 값을 더하면 0이 되므로, 남는 값은 반복이 없는 숫자가 된다.

# 결과
[Link](https://app.codility.com/demo/results/trainingPK5C7W-QF2/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson02/OddOccurrencesInArray.java){:target="_blank"}에서 확인 가능합니다.