---
title: "Leetcode Java Minimum Speed to Arrive on Time"
excerpt: "Leetcode Minimum Speed to Arrive on Time Java"
last_modified_at: 2023-07-26T20:50:00
header:
  image: /assets/images/leetcode/minimum-speed-to-arrive-on-time.png
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
[Link](https://leetcode.com/problems/minimum-speed-to-arrive-on-time){:target="_blank"}

# 코드
```java
class Solution {

  public int minSpeedOnTime(int[] dist, double hour) {
    int length = dist.length;
    int min = 1;
    int max = 10000001;
    while (min < max) {
      int mid = min + (max - min) / 2;
      double sum = 0;
      for (int i = 0; i < length - 1; i++) {
        sum += Math.ceil(((double) dist[i]) / mid);
      }
      sum += ((double) dist[length - 1]) / mid;
      if (sum > hour) {
        min = mid + 1;
      } else {
        max = mid;
      }
    }
    return min == 10000001 ? -1 : min;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-speed-to-arrive-on-time/submissions/1004408871/){:target="_blank"}

# 설명
1. dist의 각 거리를 hour시간 내 도착하기 위한 공통된 속도를 반환하는 문제이다.
- hour시간 내 도착할 수 없는 경우, -1을 반환한다.
- dist의 각 거리를 출발하기 위해서는 정수에 해당하는 시간에 출발 가능하다.
- 속도는 $10^7$을 초과할 수 없고, 소수점 뒤 최대 두 자리까지만 가능하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 dist의 길이를 저장한 변수이다.
- min과 max는 최소 속도와 최대 속도를 저장할 변수로, 1과 최대 가능한 값보다 1 큰 10000001으로 초기화한다.

3. min이 max 미만일 때까지 아래를 수행한다.
- mid에 $min + \frac{max - min}{2}$의 중앙값을 넣어준다.
- sum에 0부터 $length - 1$까지 i를 증가시키며 각 시작은 정수에 해당하는 시간에 출발 가능하므로, $\frac{dist[i]}{mid}$의 결과를 올림 처리하여 sum에 더해준다. 
- 마지막으로 도착하는 시간인 dist의 $length - 1$번째 값을 mid로 나눈 값을 더해준다.
- sum이 hour보다 큰지 검증하여 아래를 수행한다.
  - 큰 경우, min에 $mid + 1$을 넣어 범위를 좁혀준다.
  - 크지 않은 경우, max에 mid를 넣어 범위를 좁혀준다.

4. 반복이 완료되면 min이 10000001이면 속도 제한을 초과하므로 -1을, 아니면 min을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumSpeedToArriveOnTime.java){:target="_blank"}에서 확인 가능합니다.