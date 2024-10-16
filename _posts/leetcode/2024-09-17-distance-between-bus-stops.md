---
title: "Leetcode Java Distance Between Bus Stops"
excerpt: "Leetcode Distance Between Bus Stops Java"
last_modified_at: 2024-09-17T09:50:00
header:
  image: /assets/images/leetcode/distance-between-bus-stops.png
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
[Link](https://leetcode.com/problems/distance-between-bus-stops/){:target="_blank"}

# 코드
```java
class Solution {

  public int distanceBetweenBusStops(int[] distance, int start, int destination) {
    int length = distance.length;
    int forward = 0;
    int reverse = 0;
    for (int i = start; i != destination; i = (i + 1) % length) {
      forward += distance[i];
    }
    for (int i = destination; i != start; i = (i + 1) % length) {
      reverse += distance[i];
    }
    return Math.min(forward, reverse);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/distance-between-bus-stops/submissions/1392682771/){:target="_blank"}

# 설명
1. n개의 버스 정류장 사이의 거리가 각각 distance라고 할 때, start에서 destination까지 이동하기 위한 최단 거리를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- legnth는 distnace의 길이를 저장한 변수이다.
- forward는 start에서 destination까지 이동하면서 거리를 계산할 변수로, distance의 start부터 destination까지 거리의 합계를 넣어준다.
- reverse는 destination에서 start까지 이동하면서 거리를 계산할 변수로, distacne의 destiantion에서 start까지 거리의 합게를 넣어준다.

3. forward와 reverse 중 가장 빠른 경로를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DistanceBetweenBusStops.java){:target="_blank"}에서 확인 가능합니다.