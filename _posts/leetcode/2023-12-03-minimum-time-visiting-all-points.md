---
title: "Leetcode Java Minimum Time Visiting All Points"
excerpt: "Leetcode Easy - 'Minimum Time Visiting All Points' 문제 Java 풀이"
last_modified_at: 2023-12-03T09:40:00
header:
  image: /assets/images/leetcode/minimum-time-visiting-all-points.png
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
[Link](https://leetcode.com/problems/minimum-time-visiting-all-points){:target="_blank"}

# 코드
```java
class Solution {

  public int minTimeToVisitAllPoints(int[][] points) {
    int result = 0;
    for (int i = 1; i < points.length; i++) {
      int[] curr = points[i];
      int[] prev = points[i - 1];
      result += Math.max(Math.abs(curr[0] - prev[0]), Math.abs(curr[1] - prev[1]));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-time-visiting-all-points/submissions/1111143082/){:target="_blank"}

# 설명
1. points의 각 지점을 이동하기 위한 최소 시간을 구하는 문제이다.
- 모든 이동(가로, 세로, 대각)의 걸리는 시간은 1로 취급한다.

2. 시간을 계산할 result를 0으로 초기화한다.

3. 1부터 points의 길이 미만까지 반복하여 현재 위치의 x와 y값을 이전 위치의 x와 y값을 각각 뺸 값 중 큰 값을 result에 더해준다.
- 가로, 세로, 대각 이동의 시간이 동일하므로 x축과 y축에 대한 길이만 판단한다.

4. 반복이 완료되면 계산된 최소 시간인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumTimeVisitingAllPoints.java){:target="_blank"}에서 확인 가능합니다.