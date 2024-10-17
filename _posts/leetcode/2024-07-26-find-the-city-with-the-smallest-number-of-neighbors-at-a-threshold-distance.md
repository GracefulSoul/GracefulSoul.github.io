---
title: "Leetcode Java Find the City With the Smallest Number of Neighbors at a Threshold Distance"
excerpt: "Leetcode Medium - 'Find the City With the Smallest Number of Neighbors at a Threshold Distance' 문제 Java 풀이"
last_modified_at: 2024-07-26T18:30:00
header:
  image: /assets/images/leetcode/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance.png
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
[Link](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/){:target="_blank"}

# 코드
```java
class Solution {

  public int findTheCity(int n, int[][] edges, int distanceThreshold) {
    int[][] distance = new int[n][n];
    int result = 0;
    int min = n;
    for (int[] row : distance) {
      Arrays.fill(row, 10001);
    }
    for (int[] edge : edges) {
      distance[edge[0]][edge[1]] = distance[edge[1]][edge[0]] = edge[2];
    }
    for (int i = 0; i < n; i++) {
      distance[i][i] = 0;
    }
    for (int k = 0; k < n; k++) {
      for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
          distance[i][j] = Math.min(distance[i][j], distance[i][k] + distance[k][j]);
        }
      }
    }
    for (int i = 0; i < n; i++) {
      int count = 0;
      for (int j = 0; j < n; j++) {
        if (distance[i][j] <= distanceThreshold) {
          count++;
        }
      }
      if (count <= min) {
        result = i;
        min = count;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/submissions/1333931120/){:target="_blank"}

# 설명
1. n개의 도시간 연결 정보가 있는 edges를 이용하여, 도시 간 이동이 distanceThreshold 이내로 이동하여 도달할 수 있는 가장 적은 도시 중 큰 숫자의 도시를 반환하는 문제이다.
- edges[i] = [from<sub>i</sub>, to<sub>i</sub>, weight<sub>i</sub>] 로, from번째 도시에서 to번째 도시까지 거리가 weight임 의미한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- distance는 [Floyd Warshall](https://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm){:target="_blank"} 알고리즘을 이용하여 거리를 계산하기 위한 변수로, $n \times n$ 크기의 2차원 정수 배열로 초기화 후 아래를 수행한다.
  - distance의 모든 위치에 최댓값인 10000 보다 1 큰 10001을 넣어준다.
  - edges의 각 값들을 이용하여 distance[edge[0]][edge[1]], distance[edge[1]][edge[0]] 두 위치에 거리인 edge[2] 값을 넣어준다.
  - 자기 자신으로 가는 경우인 출발지와 도착지가 동일한 경우, 값을 0으로 초기화해준다.
  - 노드의 경유를 고려하여 i번째 도시에서 j번째 도시로 가는 distance[i][j]와 k를 경유하는 경우인 $distance[i][k] + distance[k][j]$ 중 최단 거리를 넣어준다.
- result는 결과를 저장하기 위한 변수로, 0으로 초기화한다.
- 최솟값을 저장하기 위한 min을 가능한 최대 도시의 값인 n으로 초기화한다.

3. 0부터 n 미만까지 i를 증가시키면서 아래를 반복한다.
- count는 각 도시로 이동 가능한 도시의 갯수를 저장할 변수로, 0으로 초기화한다.
- 0부터 n 미만까지 j를 증가시키면서 distance[i][j]의 값이 distanceThreshold 이하인 도시의 갯수를 계산한다.
- count가 min 이하이면 result에 i를, min에 count를 넣어 준다.

4. 반복이 완료되면 이동 가능한 도시가 적으면서 도시의 숫자가 가장 큰 result를 주어진 문제의 결과로 반환한다.

# 해설
- 여느 문제와 같이 도시의 숫자가 작은 값부터 이동 가능한 도시의 갯수가 동일한 경우를 포함하는 이유는, 문제의 조건인 도시의 숫자가 큰 경우만 남기기 위함이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheCityWithTheSmallestNumberOfNeighborsAtAThresholdDistance.java){:target="_blank"}에서 확인 가능합니다.