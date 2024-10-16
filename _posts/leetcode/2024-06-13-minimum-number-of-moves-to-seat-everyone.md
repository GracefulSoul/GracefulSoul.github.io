---
title: "Leetcode Java Minimum Number of Moves to Seat Everyone"
excerpt: "Leetcode Minimum Number of Moves to Seat Everyone Java"
last_modified_at: 2024-06-13T17:20:00
header:
  image: /assets/images/leetcode/minimum-number-of-moves-to-seat-everyone.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/minimum-number-of-moves-to-seat-everyone/){:target="_blank"}

# 코드
```java
class Solution {

  public int minMovesToSeat(int[] seats, int[] students) {
    Arrays.sort(seats);
    Arrays.sort(students);
    int result = 0;
    for (int i = 0; i < seats.length; i++) {
      result += Math.abs(seats[i] - students[i]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-moves-to-seat-everyone/submissions/1286834289/){:target="_blank"}

# 설명
1. students의 각 학생들이 비어있는 자리인 seats의 자리로 각자 이동할 때, 최소 이동 횟수를 구하는 문제이다.

2. seats와 students를 오름차순으로 정렬하여 좌석과 학생을 인접한 순서로 만들어준다.

3. result는 최소 이동 횟수를 계산할 변수로, seats와 students의 동일하게 위치한 값들의 차이에 대한 절댓값의 합을 더해서 넣어준 후 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfMovesToSeatEveryone.java){:target="_blank"}에서 확인 가능합니다.