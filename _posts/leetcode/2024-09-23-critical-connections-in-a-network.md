---
title: "Leetcode Java Critical Connections in a Network"
excerpt: "Leetcode Critical Connections in a Network Java"
last_modified_at: 2024-09-23T20:30:00
header:
  image: /assets/images/leetcode/critical-connections-in-a-network.png
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
[Link](https://leetcode.com/problems/critical-connections-in-a-network/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
    List<Integer>[] graph = new ArrayList[n];
    for (int i = 0; i < n; i++) {
      graph[i] = new ArrayList<>();
    }
    for (List<Integer> connection : connections) {
      graph[connection.get(0)].add(connection.get(1));
      graph[connection.get(1)].add(connection.get(0));
    }
    List<List<Integer>> results = new ArrayList<>();
    this.dfs(results, graph, 0, 0, new int[n], 1);
    return results;
  }

  private void dfs(List<List<Integer>> results, List<Integer>[] graph, int parent, int node, int[] times, int time) {
    times[node] = time;
    for (int neighbor : graph[node]) {
      if (neighbor == parent) {
        continue;
      }
      if (times[neighbor] == 0) {
        this.dfs(results, graph, node, neighbor, times, time + 1);
      }
      times[node] = Math.min(times[node], times[neighbor]);
      if (times[neighbor] > time) {
        results.add(Arrays.asList(node, neighbor));
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/critical-connections-in-a-network/submissions/1399525950/){:target="_blank"}

# 설명
1. n개의 서버들의 서버 간 연결 정보를 나타내는 connections을 이용하여 한 연결 정보를 삭제하는 경우, 둘 중 하나의 서버로 접근이 불가능한 치명적인 연결 정보를 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- graph는 서버들 간 연결 정보를 저장할 변수로, n개의 ArrayList 배열로 초기화 후 connections를 모두 반복하여 각 서버의 위치에 연결된 서버 번호를 넣어준다.
- results는 치명적인 연결 정보를 저장하기 위한 변수로, ArrayList로 초기화한다.

3. 4번에서 정의한 dfs(List<List<Integer>> results, List<Integer>[] graph, int parent, int node, int[] times, int time) 메서드를 수행하여 치명적인 연결 정보가 저장된 result를 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 치명적인 연결 정보를 탐색할 dfs(List<List<Integer>> results, List<Integer>[] graph, int parent, int node, int[] times, int time) 메서드를 정의한다.
- times[node]의 위치에 time을 넣어준다.
- graph[node]의 값들을 순차적으로 neighbor에 넣고 아래를 수행한다.
  - neighbor와 parent가 동일한 이전 경로인 경우, 다음 반복을 수행한다.
  - times[neighbor]의 값이 0인 수행되지 않은 노드인 경우, parent에 node, node에 neighbor를 넣고 time을 증가시켜 재귀 호출을 수행한다.
  - times[node]에 times[node]와 times[neighbor] 중 작은 값을 넣어준다.
  - current가 times[neighbor]보다 작은 치명적인 경로인 경우, node와 neighbor 조합을 result에 넣어준다.

# 해설 
- 치명적인 연결이 A 서버와 B 서버인 경우, B 서버로 가기 위한 연결은 반드시 A 서버를 거치는 방법이어야 한다.
- 위의 설명을 기반으로 A 서버까지 걸린 현재 시간인 current가 B가 수행되었던 times[B]보다 큰 경우, B로 갈 수 있는 서버가 또 존재하므로 치명적인 연결이 아니게 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CriticalConnectionsInANetwork.java){:target="_blank"}에서 확인 가능합니다.