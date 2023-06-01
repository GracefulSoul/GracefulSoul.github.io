---
title: "Leetcode Java Shortest Path in Binary Matrix"
excerpt: "Leetcode Shortest Path in Binary Matrix Java"
last_modified_at: 2023-06-01T19:40:00
header:
  image: /assets/images/leetcode/shortest-path-in-binary-matrix.png
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
[Link](https://leetcode.com/problems/shortest-path-in-binary-matrix){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[][] DIRECTIONS = new int[][] {
    { 0, 1 },
    { 1, 0 },
    { -1, 0 },
    { 0, -1 },
    { 1, 1 },
    { -1, 1 },
    { 1, -1 },
    { -1, -1 }
  };

  public int shortestPathBinaryMatrix(int[][] grid) {
    if (grid[0][0] == 0) {
      int length = grid.length;
      Queue<int[]> queue = new LinkedList<>();
      queue.add(new int[] { 0, 0, 0 });
      while (!queue.isEmpty()) {
        int[] curr = queue.poll();
        if (curr[0] == length - 1 && curr[1] == length - 1) {
          return curr[2] + 1;
        }
        for (int[] direction : DIRECTIONS) {
          int x = curr[0] + direction[0];
          int y = curr[1] + direction[1];
          if (x >= 0 && y >= 0 && x < length && y < length && grid[x][y] == 0) {
            grid[x][y] = -1;
            queue.add(new int[] { x, y, curr[2] + 1 });
          }
        }
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shortest-path-in-binary-matrix/submissions/961564900/){:target="_blank"}

# 설명
1. $n \times n$ 크기의 이차원 배열인 grid를 이용하여 가장 짧은 확실한 길을 찾는 문제이다.
- 확실한 길은 [0, 0] 위치에서 [$n - 1$, $n - 1$] 위치까지 이동하는 길이다.
- 이동 방향은 셀의 인접한 모든 방향 중 0인 값으로 이동 가능하다.

2. 시작 위치인 grid[0][0]이 0인 경우만 아래를 수행하고 아닌 경우, -1을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- length는 grid의 길이를 저장한 변수이다.
- queue는 이동 방향에 대한 위치 별 이동 횟수를 순차적으로 모두 탐색하기 위한 큐로, LinkedList로 초기화하고 첫 위치와 이동 횟수를 [0, 0, 0] 배열로 넣어준다.
- queur가 비어있지 않을 때 까지 아래를 반복한다.
  - curr은 queue에 있는 값을 꺼내 넣어준다.
  - [x, y]인 curr의 두 값이 $length - 1$인 경우, 이동 횟수인 curr[2]의 값에 마지막 위치로 이동하기 위한 이동 횟수인 1을 더해서 반환한다.
  - 위가 아니라면 DIRECTIONS의 8방향을 순차적으로 direction에 넣고 반복할 때, x와 y에 더해서 x와 y가 0 ~ $length - 1$ 사이 값이면서 이동 가능한 값이 0인 경우 이동 할 위치에 -1을 넣고 queue에 앞의 위치에 이동 횟수를 추가하여 다시 넣어준다.

4. 반복이 완료되면 가장 짧은 확실한 길이 존재하지 않는다는 의미이므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestPathInBinaryMatrix.java){:target="_blank"}에서 확인 가능합니다.