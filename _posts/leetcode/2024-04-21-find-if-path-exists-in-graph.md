---
title: "Leetcode Java Find if Path Exists in Graph"
excerpt: "Leetcode Find if Path Exists in Graph Java"
last_modified_at: 2024-04-21T19:30:00
header:
  image: /assets/images/leetcode/find-if-path-exists-in-graph.png
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
[Link](https://leetcode.com/problems/find-if-path-exists-in-graph/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean validPath(int n, int[][] edges, int source, int destination) {
    if (edges.length == 0) {
      return true;
    } else {
      boolean[] visited = new boolean[n];
      visited[source] = true;
      boolean running = true;
      while (running) {
        running = false;
        for (int[] edge : edges) {
          if (visited[edge[0]] != visited[edge[1]]) {
            visited[edge[0]] = true;
            visited[edge[1]] = true;
            running = true;
          }
          if (visited[destination]) {
            return true;
          }
        }
      }
      return false;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-if-path-exists-in-graph/submissions/1238132601/){:target="_blank"}

# 설명
1. n개의 점에서 연결선인 edges를 이용하여 source에서 destination까지 연결이 가능한지 여부를 판단하는 문제이다.
- 각 점은 다른 점과의 연결선이 존재하고, 자기 자신과 연결되는 선은 존재하지 않는다.

2. edges의 길이가 0인 경우, 연결선이 없으므로 true를 반환한다.

3. 2번의 경우가 아닌 경우, 아래를 수행한다.
- visited는 해당 위치의 점을 탐색한 이력을 저장할 배열로, n 크기의 부울 변수로 정의하고 source번째 자리만 true로 초기화한다.
- running은 계속 진행할지 여부를 저장할 변수로, true로 초기화한다.

4. running이 true일 때 까지 아래를 반복한다.
- running을 false로 바꾸어주고, edges를 순차적으로 edge에 넣어 아래를 반복한다.
  - visited의 edge[0]번째 값이 edge[1]번째 값과 다르면 이미 탐색한 경로가 아니므로, 두 위치에 true를 넣고 running을 true로 바꾸어 탐색을 진행한다.
  - visited의 destination번째 값이 true인 목표에 도달한 경우, true를 반환한다.

5. 반복이 모두 완료되어 목표에 도달하는 경로가 없으면, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindIfPathExistsInGraph.java){:target="_blank"}에서 확인 가능합니다.