---
title: "Leetcode Java Is Graph Bipartite?"
excerpt: "Leetcode Is Graph Bipartite? Java"
last_modified_at: 2022-12-28T16:00:00
header:
  image: /assets/images/leetcode/is-graph-bipartite.png
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
[Link](https://leetcode.com/problems/is-graph-bipartite){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isBipartite(int[][] graph) {
    int[] sets = new int[graph.length];
    for (int idx = 0; idx < graph.length; idx++) {
      if (sets[idx] == 0 && !this.dfs(graph, sets, 1, idx)) {
        return false;
      }
    }
    return true;
  }

  private boolean dfs(int[][] graph, int[] sets, int set, int index) {
    if (sets[index] != 0) {
      return sets[index] == set;
    }
    sets[index] = set;
    for (int node : graph[index]) {
      if (!this.dfs(graph, sets, -set, node)) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/letter-case-permutation/submissions/866187282/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 n개의 노드들의 정보인 graph를 이용하여 두 그룹으로 나눌 때 맨 앞과 끝의 노드가 다른 그룹으로 이어져 분리할 수 있는지를 검증하는 문제이다.
- 자기 자신 노드와 연결되는 노드는 없다.
- 한 노드에서 다음 노드로 병렬 연결된 노드는 없다.
- graph[u]에 'v'가 포함된 경우, graph[v]에 'u'가 포함되어있다. (단, 방향은 지정되어 있지 않다.)
- graph의 각 노드들은 연결되어 있지 않을 수 있다. 

2. sets는 각 노드 별 아래와 같은 값의 구분을 통해 그룹을 지정할 배열로, graph의 길이 크기로 초기화한다.
- '0'은 그룹을 지정하지 않은 노드이다.
- '1'은 그룹 A를 의미한다.
- '-1'은 그룹 B를 의미한다.

3. 0부터 graph의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- 아래의 조건을 모두 만족하는 경우, 주어진 조건에 따른 두 그룹으로 분리할 수 없으므로 false를 주어진 문제의 결과로 반환한다.
  - sets의 idx번째 값이 0인 그룹을 지정하지 않은 노드인 경우.
  - 4번에서 정의한 dfs(graph, sets, 1, idx) 메서드의 수행 결과가 false인 분리 불가능한 노드인 경우.

4. DFS 방식으로 조건에 따른 그룹 분리가 가능한지 검증하기 위한 dfs(graph, sets, 1, idx) 메서드를 정의한다.
- sets의 index번째 그룹이 0이 아닌 경우, 해당 위치의 값이 set인지 검증한 결과를 반환한다.
- sets의 index번째 그룹에 set을 넣어 그룹을 분류한다.
- graph의 index번째 노드 정보들을 node에 넣어 아래를 반복 수행한다.
  - set의 값을 다른 그룹 값으로 전환하여 재귀 호출을 수행한 결과가 false인 경우, 조건에 따른 분리가 불가능하므로 false를 반환한다.
- 위의 모든 절차가 완료되면 index번째 노드의 위치에서 검증이 완료되었으므로 true를 반환한다.

5. 3번의 반복이 완료되면 조건에 따른 분리가 가능한 것으로 검증되었으므로 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IsGraphBipartite.java){:target="_blank"}에서 확인 가능합니다.