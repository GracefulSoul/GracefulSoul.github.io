---
title: "Leetcode Java All Ancestors of a Node in a Directed Acyclic Graph"
excerpt: "Leetcode Medium - 'All Ancestors of a Node in a Directed Acyclic Graph' 문제 Java 풀이"
last_modified_at: 2024-06-29T09:50:00
header:
  image: /assets/images/leetcode/all-ancestors-of-a-node-in-a-directed-acyclic-graph.png
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
[Link](https://leetcode.com/problems/all-ancestors-of-a-node-in-a-directed-acyclic-graph/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> getAncestors(int n, int[][] edges) {
    List<List<Integer>> result = new ArrayList<>();
    List<List<Integer>> childs = new ArrayList<>();
    for (int i = 0; i < n; i++) {
      result.add(new ArrayList<>());
      childs.add(new ArrayList<>());
    }
    for (int[] edge : edges) {
      childs.get(edge[0]).add(edge[1]);
    }
    for (int i = 0; i < n; i++) {
      this.dfs(result, childs, i, i);
    }
    return result;
  }

  private void dfs(List<List<Integer>> result, List<List<Integer>> childs, int node, int curr) {
    for (int child : childs.get(curr)) {
      List<Integer> list = result.get(child);
      if (list.size() == 0 || list.get(list.size() - 1) != node) {
        list.add(node);
        this.dfs(result, childs, node, child);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-total-importance-of-roads/submissions/1303004475/){:target="_blank"}

# 설명
1. 노드 간 연결 선 목록인 edge를 이용하여 각 노드들로 이동 가능한 노드들의 목록을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 각 노드들로 이동 가능한 노드들을 저장하기 위한 변수로, ArrayList로 초기화하고 n개의 ArrayList를 넣어준다.
- childs는 각 노드가 이동하는 경로를 넣어줄 변수로, ArrayList로 초기화하고 edges를 이용하여 첫 번째 값에 해당하는 ArrayList에 두 번째 값을 넣어준다.

3. 0부터 n까지 i를 증가시키며 4번에서 정의한 dfs(List<List<Integer>> result, List<List<Integer>> childs, int node, int curr) 메서드의 node와 curr에 i를 넣고 수행한다.

4. DFS 방식으로 각 노드로 이동 가능한 노드들을 탐색할 dfs(List<List<Integer>> result, List<List<Integer>> childs, int node, int curr) 메서드를 정의한다.
- childs의 curr에 해당하는 노드들을 순차적으로 child에 넣어 아래를 수행한다.
  - list에 result의 child번째 ArrayList를 꺼내 넣어준다.
  - list가 비어있거나 list의 마지막 값이 node가 아닌 이동 가능한 경로인 경우, list에 node를 넣고 curr 자리에 child를 넣어 재귀 호출을 수행한다.

5. 수행이 완료되어 모든 이동 가능한 노드들이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AllAncestorsOfANodeInADirectedAcyclicGraph.java){:target="_blank"}에서 확인 가능합니다.