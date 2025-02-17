---
title: "Leetcode Java Airplane Seat Assignment Probability"
excerpt: "Leetcode - 'Airplane Seat Assignment Probability' 문제 Java 풀이"
last_modified_at: 2025-02-17T18:40:00
header:
  image: /assets/images/leetcode/airplane-seat-assignment-probability.png
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
[Link](https://leetcode.com/problems/airplane-seat-assignment-probability/){:target="_blank"}

# 코드
```java
class Solution {

  public double nthPersonGetsNthSeat(int n) {
    return n == 1 ? 1.0d : 0.5d;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/airplane-seat-assignment-probability/submissions/1546050865/){:target="_blank"}

# 설명
1. n번째 승객이 n석이 존재하는 비행기에 탑승할 때, 각 승객이 임의 좌석에 앉을 경우 자기 자신의 좌석에 앉을 확률을 구하는 문제이다.

2. 첫 손님은 첫 자리에 앉을 수 있으므로 1을, 그 외는 0.5를 주어진 문제의 결과로 반환한다.
- n이 2인 경우, $f(2) = \frac{1}{2}$를 만족하는 것을 알 수 있다.
- 위를 이용하여 $f(m + 1) = \frac{1}{m + 1} + \frac{m + 1 - 2}{m + 1} \times f(m) = \frac{2}{2 \times (m + 1)} + \frac{m - 1}{m + 1} \times \frac{1}{2} = \frac{m + 1}{2 \times (m + 1)} = \frac{1}{2}$를 만족하므로, n이 1이 아닌 결과는 모두 0.5가 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AirplaneSeatAssignmentProbability.java){:target="_blank"}에서 확인 가능합니다.