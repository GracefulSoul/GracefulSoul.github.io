---
title: "Leetcode Java Minimum Obstacle Removal to Reach Corner"
excerpt: "Leetcode - 'Minimum Obstacle Removal to Reach Corner' 문제 Java 풀이"
last_modified_at: 2024-11-28T20:00:00
header:
  image: /assets/images/leetcode/minimum-obstacle-removal-to-reach-corner.png
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
[Link](https://leetcode.com/problems/minimum-obstacle-removal-to-reach-corner/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[][] DIRECTIONS = {
    { 0, 1 },
    { 1, 0 },
    { 0, -1 },
    { -1, 0 }
  };

  public int minimumObstacles(int[][] grid) {
    int row = grid.length;
    int col = grid[0].length;
    Deque<int[]> deque = new ArrayDeque<>();
    deque.add(new int[] { 0, 0, 0 });
    grid[0][0] = -1;
    while (!deque.isEmpty()) {
      int[] curr = deque.pollFirst();
      int x = curr[0];
      int y = curr[1];
      int obstacle = curr[2];
      if (x == row - 1 && y == col - 1) {
        return obstacle;
      }
      for (int[] direction : DIRECTIONS) {
        int dx = x + direction[0];
        int dy = y + direction[1];
        if (0 <= dx && dx < row && 0 <= dy && dy < col && grid[dx][dy] != -1) {
          if (grid[dx][dy] == 0) {
            deque.addFirst(new int[] { dx, dy, obstacle });
          } else {
            deque.addLast(new int[] { dx, dy, obstacle + 1 });
          }
          grid[dx][dy] = -1;
        }
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-obstacle-removal-to-reach-corner/submissions/1464965130/){:target="_blank"}

# 설명
1. 이차원 배열 grid에서 아래 규칙을 따라 좌측 상단의 [0, 0] 위치에서 우측 하단의 [$m - 1$, $n - 1$]로 이동하기 위해 제거할 최소 장애물 갯수를 구하는 문제이다.
- grid[i]의 값이 0이면 빈 셀을 의미한다.
- grid[i]의 값이 1이면 장애물을 의미한다.
- 빈 셀에서 상하좌우로 이동이 가능하다.

2. DIRECTIONS는 grid에서 이동하기 위한 상하좌우 방향의 가감치를 저장한 전역 변수이다.

3. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 grid의 행과 열의 길이를 저장한 변수이다.
- deque는 위치를 이동하며 제거할 최소 장애물을 계산하기 위한 변수로, ArrayDeque로 초기화하여 첫 값을 시작 위치와 이동 거리인 [0, 0, 0]으로 초기화한다.
- grid[0][0] 위치에 -1을 넣어 방문한 위치를 표시한다.

4. deque의 값이 존재할 때 까지 아래를 반복한다.
- curr에 deque의 처음 배열을 꺼내 행 위치인 x에 curr[0], 열 위치인 y에 curr[1], 제거할 장애물 갯수인 obstacle에 curr[2]를 넣어준다.
- [x, y]의 값이 우측 하단의 목표 지점인 경우, 제거할 장애물의 갯수인 obstacle을 주어진 문제의 결과로 반환한다.
- DIRECTIONS의 각 값을 순차적으로 direction에 넣어 아래를 수행한다.
  - dx에 $x + direction[0]$, dy에 $y + direction[1]$의 값을 넣어준다.
  - dx와 dy가 범위 내에 존재하면서 grid[dx][dy]의 값이 -1이 아닌 방문하지 않은 위치인 경우, grid[dx][dy]가 빈 셀인 0이면 deque의 첫 위치에 [dx, dy, obstacle]을, 1이면 deque의 마지막 위치에 제거할 장애물이 추가되었으므로 [dx, dy, $obstacle + 1$]을 넣어준다.
- grid[dx][dy]에 -1을 넣어 방문한 위치를 표시한다.

5. 위의 수행에서 제거할 장애물 갯수에 제한이 없어 반드시 결과가 반환되므로, 임의 값인 -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumObstacleRemovalToReachCorner.java){:target="_blank"}에서 확인 가능합니다.