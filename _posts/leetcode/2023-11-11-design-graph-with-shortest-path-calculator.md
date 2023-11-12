---
title: "Leetcode Java Design Graph With Shortest Path Calculator"
excerpt: "Leetcode Design Graph With Shortest Path Calculator Java"
last_modified_at: 2023-11-11T12:00:00
header:
  image: /assets/images/leetcode/design-graph-with-shortest-path-calculator.png
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
[Link](https://leetcode.com/problems/design-graph-with-shortest-path-calculator){:target="_blank"}

# 코드
```java
class Graph {

  private int n;
  private int[][] costs;

  public Graph(int n, int[][] edges) {
    this.costs = new int[n][n];
    this.n = n;
    for (int[] a : this.costs) {
      Arrays.fill(a, (int) 1e9);
    }
    for (int[] e : edges) {
      this.costs[e[0]][e[1]] = e[2];
    }
    for (int i = 0; i < n; i++) {
      this.costs[i][i] = 0;
    }
    for (int k = 0; k < n; k++) {
      for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
          this.costs[i][j] = Math.min(this.costs[i][j], this.costs[i][k] + this.costs[k][j]);
        }
      }
    }
  }

  public void addEdge(int[] e) {
    for (int i = 0; i < this.n; i++) {
      for (int j = 0; j < this.n; j++) {
        this.costs[i][j] = Math.min(this.costs[i][j], this.costs[i][e[0]] + this.costs[e[1]][j] + e[2]);
      }
    }
  }

  public int shortestPath(int node1, int node2) {
    if (this.costs[node1][node2] >= (int) 1e9) {
      return -1;
    } else {
      return this.costs[node1][node2];
    }
  }

}

/**
 * Your Graph object will be instantiated and called as such:
 * Graph obj = new Graph(n, edges);
 * obj.addEdge(edge);
 * int param_2 = obj.shortestPath(node1,node2);
 */
```

# 결과
[Link](https://leetcode.com/problems/design-graph-with-shortest-path-calculator/submissions/1096303292/){:target="_blank"}

# 설명
1. [0, $n - 1$]까지 노드간 최단 길이를 찾을 수 있는 Graph 객체를 완성하는 문제이다.
- edge[i] = [from<sub>i</sub>, to<sub>i</sub>, edgeCost<sub>i</sub>]로, from<sub>i</sub>에서 to<sub>i</sub>로 가는데 걸리는 비용이 edgeCost<sub>i</sub>임을 나타낸다.
- 생성자인 Graph(int n, int[][] edges)는, n과 edges를 이용하여 Graph 객체를 초기화하는 역할을 수행한다.
- 메서드인 addEdge(int[] edge)는, 이전까지 존재하지 않는 edge를 Graph 객체에 추가하는 역할을 수행한다.
- 메서드인 shortestPath(int node1, int node2)는, node1부터 node2까지 가장 짧은 비용을 반환하는 역할을 수행한다. 단, 경로가 존재하지 않으면 -1을 반환한다.

2. Graph의 객체에 필요한 전역 변수를 정의한다.
- n은 노드의 갯수를 저장할 변수이다.
- costs는 노드 간 비용을 저장할 변수이다.

3. 생성자인 Graph(int n, int[][] edges)를 초기화한다.
- n을 전역 변수 n에 넣어준다.
- 전역 변수 cost에 한 노드에서 다른 노드로 이동하기 위한 비용을 저장하기 위해서, 2차원 배열로 초기화하고 모든 값에 노드 간 길이의 상한값인 $10^9$를 넣어준다.
- costs의 내 모든 노드가 자기 자신의 노드로 이동하는 costs[i, i]에 0을 넣어준다.
- k, i, j 순으로 0부터 n 미만까지 k, i, j를 각각 증가시키며 아래를 반복한다.
- costs[i][j]에 자기 자신의 값과 $cost[i][k] + cost[k][j]$인 k를 경유하고 이동한 값 중 가장 작은 값을 넣어준다.

4. 메서드인 addEdge(int[] edge)를 초기화한다.
- i, j 순으로 0부터 n 미만까지 i, j를 각각 증가시키며 아래를 반복한다.
  - costs[i][j]에 자기 자신의 값과 $costs[i][e[0]] + csts[e[1]][j] + e[2]$인 엣지 라인을 경유하고 가는 경우의 비용 중 작은 값을 넣어주낟.

5. 메서드인 shortestPath(int node1, int node2)를 초기화한다.
- costs[node1][node2]가 $10^9$보다 큰 경우, 루트가 존재하지 않으므로 -1을 반환한다.
- 위의 경우가 아니라면 costs[node1][node2]의 비용을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignGraphWithShortestPathCalculator.java){:target="_blank"}에서 확인 가능합니다.