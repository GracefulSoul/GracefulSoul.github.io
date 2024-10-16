---
title: "Leetcode Java Sum of Distances in Tree"
excerpt: "Leetcode Sum of Distances in Tree Java"
last_modified_at: 2023-02-09T21:15:00
header:
  image: /assets/images/leetcode/sum-of-distances-in-tree.png
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
[Link](https://leetcode.com/problems/sum-of-distances-in-tree){:target="_blank"}

# 코드
```java
class Solution {

  public int[] sumOfDistancesInTree(int n, int[][] edges) {
    int[] count = new int[n];
    Arrays.fill(count, 1);
    int[] result = new int[n];
    List<Integer>[] graph = new ArrayList[n];
    for (int i = 0; i < n; i++) {
      graph[i] = new ArrayList<>();
    }
    for (int[] edge : edges) {
      graph[edge[0]].add(edge[1]);
      graph[edge[1]].add(edge[0]);
    }
    this.postOrderDFS(graph, count, result, 0, -1);
    this.preOrderDFS(graph, n, count, result, 0, -1);
    return result;
  }

  private void postOrderDFS(List<Integer>[] graph, int[] count, int[] result, int a, int parent) {
    for (int b : graph[a]) {
      if (b != parent) {
        this.postOrderDFS(graph, count, result, b, a);
        count[a] += count[b];
        result[a] += result[b] + count[b];
      }
    }
  }

  private void preOrderDFS(List<Integer>[] graph, int n, int[] count, int[] result, int a, int parent) {
    for (int b : graph[a]) {
      if (b != parent) {
        result[b] = result[a] + (n - count[b]) - count[b];
        this.preOrderDFS(graph, n, count, result, b, a);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sum-of-distances-in-tree/submissions/894679668/){:target="_blank"}

# 설명
1. n개의 노드의 연결 정보가 담긴 edges를 이용하여 각 노드의 위치에서 다른 노드의 거리 합을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 각 노드 위치에서 하위의 모든 노드의 개수를 저장하기 위한 배열로, n 크기의 정수 배열로 초기화하고 모든 위치에 1을 넣어준다.
- result는 각 노드 위치에서 하위의 모든 노드의 거리의 합을 저장하기 위한 배열로, n 크기의 정수 배열로 초기화한다.
- graph는 각 노드가 연결된 노드를 저장하기 위한 List 배열로, n 크기의 배열로 초기화하여 모든 위치에 새 ArrayList를 넣어준다.

3. edges의 모든 값을 반복하여 graph의 edge[0]번째 ArrayList에 edge[1]을, graph의 edge[1]번째 ArrayList에 edge[0]을 넣어 서로 연결된 노드로 설정한다.

4. Post Order 방식으로 DFS를 수행하여 count와 result의 값들을 넣어주기 위한 postOrderDFS(List<Integer>[] graph, int[] count, int[] result, int a, int parent) 메서드를 정의한다.
- graph의 a번째 위치의 값들을 각각 b에 넣어 아래를 반복한다.
  - b가 상위 노드인 parent이면 반복을 계속 수행한다.
  - a의 위치에 b를, parent 위치에 a를 넣고 재귀 호출을 수행한다.
  - count의 a번째 위치에 count의 b번째 값을 더해 하위 노드의 숫자를 더해준다.
  - result의 a번째 위치에 b의 하위 노드들의 거리 합인 result의 b번째 값과 하위 노드의 개수인 count의 b번째 값을 더해준다.

5. Pre Order 방식으로 DFS를 수행하여 result의 값을 결정하기 위한 preOrderDFS(List<Integer>[] graph, int n, int[] count, int[] result, int a, int parent) 메서드를 정의한다.
- graph의 a번째 위치의 값들을 각각 b에 넣어 아래를 반복한다.
  - b가 상위 노드인 parent이면 반복을 계속 수행한다.
  - result의 b번째 위치에 result의 a번째 값과 n과 count의 b번째 값의 차이를 더한 후, count의 b번째 값을 뺀 결과를 넣어 root에 가까운 위치의 보정 값을 넣어준다.
  - $n - count[b]$는 a보다 b가 root에 1 더 가까운 값이며, count[b]는 b가 a보다 root에 1 더 가까운 값이다.

6. 4번에서 정의한 postOrderDFS(List<Integer>[] graph, int[] count, int[] result, int a, int parent) 메서드를 수행하고, 5번에서 정의한 preOrderDFS(List<Integer>[] graph, int n, int[] count, int[] result, int a, int parent) 메서드를 순차적으로 수행한다.

7. 수행이 완료되면 각 노드의 위치에서 다른 노드의 거리 합이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfDistancesInTree.java){:target="_blank"}에서 확인 가능합니다.