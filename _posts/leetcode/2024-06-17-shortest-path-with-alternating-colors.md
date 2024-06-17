---
title: "Leetcode Java Shortest Path with Alternating Colors"
excerpt: "Leetcode Shortest Path with Alternating Colors Java"
last_modified_at: 2024-06-17T19:00:00
header:
  image: /assets/images/leetcode/shortest-path-with-alternating-colors.png
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
[Link](https://leetcode.com/problems/shortest-path-with-alternating-colors/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] shortestAlternatingPaths(int n, int[][] redEdges, int[][] blueEdges) {
    Set<Integer>[][] set = new Set[n][2];
    for (int i = 0; i < n; i++) {
      set[i][0] = new HashSet<>();
      set[i][1] = new HashSet<>();
    }
    for (int[] redEdge : redEdges) {
      set[redEdge[0]][0].add(redEdge[1]);
    }
    for (int[] blueEdge : blueEdges) {
      set[blueEdge[0]][1].add(blueEdge[1]);
    }
    int[][] paths = new int[n][2];
    for (int i = 1; i < n; i++) {
      paths[i][0] = paths[i][1] = n * 2;
    }
    Queue<int[]> queue = new LinkedList<>();
    queue.offer(new int[] { 0, 0 });
    queue.offer(new int[] { 0, 1 });
    while (!queue.isEmpty()) {
      int[] curr = queue.poll();
      int row = curr[0];
      int col = curr[1];
      for (int node : set[row][1 - col]) {
        if (paths[node][1 - col] == n * 2) {
          paths[node][1 - col] = paths[row][col] + 1;
          queue.offer(new int[] { node, 1 - col });
        }
      }
    }
    int[] result = new int[n];
    for (int i = 0; i < n; i++) {
      int min = Math.min(paths[i][0], paths[i][1]);
      result[i] = min == n * 2 ? -1 : min;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shortest-path-with-alternating-colors/submissions/1291066563/){:target="_blank"}

# 설명
1. n개의 노드의 각 색깔별 이동 경로가 저장된 redEdges와 blueEdges를 이용하여 색을 번갈아가면서 0번 노드에서 각 노드까지 최단 경로를 구하는 문제이다.
- 단, 경로가 존재하지 않으면 -1을 넣어준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- set은 노드 별 도착 노드를 저장할 변수로, red와 blue를 순차적으로 넣기 위해 $n \times 2$ 크기의 Set 배열로 정의하여 redEdges는 노드 별 첫 번째 HashSet에 blueEdges는 노드 별 두 번째 HashSet에 도착 노드를 넣어준다.
- paths는 노드 별 색깔을 번갈아 이동하기 위한 횟수를 저장할 변수로, $n \times 2$ 크기의 2차원 정수 배열로 초기화하고 모든 값에 최대 가능한 경우보다 큰 $n \times 2$를 넣어준다.
  - 최대 가능한 경우는 노드로 이동하는 경로와 자기 자신을 회귀하는 아래의 경우와 같다.
  - n = 3, redEdges = [[0, 1], [1, 2]], blueEdges = [[1, 1]] 일때, 0에서 2까지 최소 3번의 단계를 거친다.
  - 위를 기반으로 $(2 \times(n - 2)) + 1 = (n \times 2) - 3$이 최소 이동 횟수가 된다.
- queue는 redEdges와 blueEdges를 순차적으로 탐색하기 위한 변수로, LinkedList로 초기화 후 [0, 0]과 [0, 1]을 순차적으로 넣어준다.

3. queue가 비어있지 않을 때 까지 아래를 반복한다.
- curr은 현재 순서를 저장할 변수로, queue의 첫 값을 빼서 넣어준다.
- row와 col은 curr의 첫 번째 값과 두 번째 값을 순차적으로 넣은 변수이다.
- set[row][$1 - col$]의 값을 순차적으로 node에 넣어 아래를 수행한다.
  - paths[node][$1 - col$]의 값이 초기 값인 $n \times 2$인 경우, paths[node][$1 - col$]의 위치에 path[row][col]의 값에 1을 더한 값을 넣어 준 후 queue에 [node, $1 - col$]을 넣어준다.

4. result는 각 노드까지 최단 경로를 저장할 변수로, n 크기의 정수 배열로 초기화한다.

5. result의 i번째 위치에 paths의 i번째 위치에 해당하는 두 경로 중 작은 값을 넣은 후 주어진 문제의 결과로 반환한다.
- 단, 가장 작은 값이 초기값인 $n \times 2$면 경로가 없으므로 -1을 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestPathWithAlternatingColors.java){:target="_blank"}에서 확인 가능합니다.