---
title: "Leetcode Java Network Delay Time"
excerpt: "Leetcode Network Delay Time Java"
last_modified_at: 2022-11-30T10:50:00
header:
  image: /assets/images/leetcode/network-delay-time.png
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
[Link](https://leetcode.com/problems/network-delay-time){:target="_blank"}

# 코드
```java
class Solution {

  public int networkDelayTime(int[][] times, int n, int k) {
    int[][] graph = new int[n][n];
    for (int idx = 0; idx < n; idx++) {
      Arrays.fill(graph[idx], Integer.MAX_VALUE);
    }
    for (int[] time : times) {
      graph[time[0] - 1][time[1] - 1] = time[2];
    }
    int[] distances = new int[n];
    Arrays.fill(distances, Integer.MAX_VALUE);
    distances[k - 1] = 0;
    boolean[] visited = new boolean[n];
    for (int i = 0; i < n; i++) {
      int index = this.findMinimumIndex(distances, visited);
      if (index == -1) {
        continue;
      }
      visited[index] = true;
      for (int j = 0; j < n; j++) {
        if (graph[index][j] != Integer.MAX_VALUE) {
          int distance = graph[index][j] + distances[index];
          if (distance < distances[j]) {
            distances[j] = distance;
          }
        }
      }
    }
    int result = 0;
    for (int distance : distances) {
      if (distance == Integer.MAX_VALUE) {
        return -1;
      }
      result = Math.max(result, distance);
    }
    return result;
  }

  private int findMinimumIndex(int[] distances, boolean[] visited) {
    int min = Integer.MAX_VALUE;
    int index = -1;
    for (int idx = 0; idx < distances.length; idx++) {
      if (!visited[idx] && distances[idx] < min) {
        min = distances[idx];
        index = idx;
      }
    }
    return index;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/852045368/){:target="_blank"}

# 설명
1. n개의 노드로 이루어진 네트워크에 1부터 n까지 레이블이 지정되면, 노드 k부터 n개의 모든 노드가 신호를 수신하는데 필요한 최소 시간을 반환한다.
- 단, n 개의 노드가 모두 신호를 수신할 수 없는 경우, -1을 주어진 문제의 결과로 반환한다.
- times[i] = (u<sub>i</sub>, v<sub>i</sub>, w<sub>i</sub>) 이며 각 값은 아래를 의미한다.
  - u<sub>i</sub>는 시작 노드를 의미한다.
  - v<sub>i</sub>는 도착 노드를 의미한다.
  - w<sub>i</sub>는 시작 노드에서 도착 노드까지 신호를 보내는데 걸리는 시간을 의미한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- graph는 n개의 노드 정보를 넣을 배열로, $n \times n$ 크기의 2차원 정수 배열로 정의하고 아래를 수행한다.
  - times의 모든 값을 이용하여 times[i]인 경우, graph[u<sub>i</sub>][v<sub>i</sub>]에 w<sub>i</sub>를 넣어준다.
  - 위의 값이 존재하지 않는 모든 위치에 빈 값을 정수의 최댓 값을 넣어 존재하지 않은 노드임을 체크해준다.
- distances는 각 노드 별 거리를 저장하기 위한 배열로, n 크기의 정수 배열로 초기화하고 아래를 수행한다.
  - 노드의 시작 위치인 $k - 1$에는 0을 넣어준다.
  - 시작 위치가 아닌 모든 위치의 값에는 최댓 값을 모두 넣어준다.
- visited는 노드의 방문 여부를 기록하기 위한 배열로, n 크기의 부울 배열로 초기화한다.

3. 최소 거리의 위치를 탐색하기 위한 findMinimumIndex(int[] distances, boolean[] visited) 메서드를 정의한다.
- 위치 탐색에 필요한 변수를 정의한다.
  - min은 최소 거리를 넣을 변수로, 정수의 최댓값으로 초기화한다.
  - index는 최소 거리 위치를 넣을 위치로, -1로 초기화한다.
- 0 부터 distnaces의 길이 미만까지 idx를 증가시키며, 방문하지 않은 최소 거리의 노드의 위치를 탐색한다.
- 탐색된 노드의 위치인 index를 반환한다.

4. 0 부터 n 미만까지 i를 증가시키며 아래를 반복한다.
- index에 3번에서 정의한 findMinimumIndex(int[] distances, boolean[] visited) 메서드를 수행한 결과인 위치 값을 넣어주고, 해당 노드의 위치가 존재하지 않는 -1이면 다음 반복을 수행한다.
- 위가 아닌경우 visited의 index번째 값에 true를 넣어 방문했다는 것을 체크해준다.
- 0부터 n 미만까지 j를 증가시키며 아래를 다시 반복한다.
  - graph[index][j]의 값이 정수 최댓값이 아닌 존재하는 노드인 경우, graph[index][j]의 값과 distances[index]의 값이 distances[j]보다 작은지 검증하여 더 거리가 짧은 경우 distances[j]에 계산된 값을 넣어준다.

5. 4번의 반복이 완료되면 result에 0을 넣고 distances를 반복하여 아래를 확인한다.
- distances에 정수의 최댓 값이 있는 경우 연결되지 않은 노드가 존재하므로, -1을 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니라면 distances 내 최댓값인 모든 노드의 반복된 시간을 찾아 result에 넣어준다.

6. 5번의 반복이 완료되면 모든 노드가 신호를 수신하는 최소 시간인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NetworkDelayTime.java){:target="_blank"}에서 확인 가능합니다.