---
title: "Leetcode Java All Paths From Source to Target"
excerpt: "Leetcode All Paths From Source to Target Java"
last_modified_at: 2023-01-09T20:55:00
header:
  image: /assets/images/leetcode/all-paths-from-source-to-target.png
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
[Link](https://leetcode.com/problems/all-paths-from-source-to-target){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
    List<List<Integer>> result = new ArrayList<>();
    this.dfs(result, new ArrayList<>(), graph, 0, graph.length - 1);
    return result;
  }

  private void dfs(List<List<Integer>> result, List<Integer> path, int[][] graph, int start, int end) {
    path.add(start);
    if (start == end) {
      result.add(new ArrayList<>(path));
    } else {
      for (int node : graph[start]) {
        this.dfs(result, path, graph, node, end);
      }
    }
    path.remove(path.size() - 1);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/all-paths-from-source-to-target/submissions/874705005/){:target="_blank"}

# 설명
1. [0, $n - 1$] 까지 값을 가진 n개 노드의 [Directed Acyclic Graph(DAG)](https://en.wikipedia.org/wiki/Directed_acyclic_graph){:target="_blank"}가 주어지면 값이 0인 노드에서 $n - 1$까지 도달하기 위한 모든 경로를 찾는 문제이다.

2. 결과를 넣을 result를 ArrayList로 초기화하여 3번의 dfs(List<List<Integer>> result, List<Integer> path, int[][] graph, int start, int end) 메서드를 수행해준다.

3. DFS 방식으로 경로를 찾기 위한 dfs(List<List<Integer>> result, List<Integer> path, int[][] graph, int start, int end) 메서드를 정의한다.
- path에 start를 넣어준다.
- start와 end가 동일한 마지막 위치인 경우, result에 path를 Deep copy하여 넣어준다.
- 위의 경우가 아니라면 graph의 start번째 노드 값의 경로를 가져와 node에 넣어 start 자리에 해당 값으로 재귀 호출을 수행한다.
- path에서 마지막 값을 제거한다.

4. 수행이 완료되어 모든 경로가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AllPathsFromSourceToTarget.java){:target="_blank"}에서 확인 가능합니다.