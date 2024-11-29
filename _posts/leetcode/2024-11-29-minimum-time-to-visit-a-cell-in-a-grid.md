---
title: "Leetcode Java Minimum Time to Visit a Cell In a Grid"
excerpt: "Leetcode - 'Minimum Time to Visit a Cell In a Grid' 문제 Java 풀이"
last_modified_at: 2024-11-29T12:00:00
header:
  image: /assets/images/leetcode/minimum-time-to-visit-a-cell-in-a-grid.png
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
[Link](https://leetcode.com/problems/minimum-time-to-visit-a-cell-in-a-grid/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[][] DIRECTIONS = new int[][] {
    { 1, 0 },
    { -1, 0 },
    { 0, 1 },
    { 0, -1 }
  };

  public int minimumTime(int[][] grid) {
    if (grid[0][1] > 1 && grid[1][0] > 1) {
      return -1;
    }
    int row = grid.length;
    int col = grid[0].length;
    Queue<int[]> queue = new PriorityQueue<>((a, b) -> a[2] - b[2]);
    queue.offer(new int[] { 0, 0, 0 });
    boolean[][] visited = new boolean[row][col];
    visited[0][0] = true;
    while (!queue.isEmpty()) {
      int[] curr = queue.poll();
      int x = curr[0];
      int y = curr[1];
      int time = curr[2];
      for (int[] direction : DIRECTIONS) {
        int dx = x + direction[0];
        int dy = y + direction[1];
        if (0 <= dx && dx < row && 0 <= dy && dy < col && !visited[dx][dy]) {
          int currTime = time + 1;
          if (grid[dx][dy] > currTime) {
            currTime += ((grid[dx][dy] - currTime + 1) / 2) * 2;
          }
          if (dx == row - 1 && dy == col - 1) {
            return currTime;
          }
          queue.offer(new int[] { dx, dy, currTime });
          visited[dx][dy] = true;
        }
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-time-to-visit-a-cell-in-a-grid/submissions/1465438735/){:target="_blank"}

# 설명
1. 이차원 정수 배열인 grid의 좌측 상단인 첫 위치에서 우측 하단의 마지막 위치까지 아래의 규칙으로 이동하기 위한 최소 시간을 계산하는 문제이다.
- 0초부터 시작하여 상하좌우 네 방향으로 이동이 가능하며, 이동에는 1초가 소요된다.
- 이동은 현재 시간 이하의 값인 위치로만 이동이 가능하다.
- 마지막 위치로 이동이 불가능한 경우, -1을 주어진 문제의 결과로 반환한다.

2. DIRECTIONS는 grid에서 이동하기 위한 상하좌우 방향의 가감치를 저장한 전역 변수이다.

3. grid[0][1] 혹은 grid[1][0]의 값이 1보다 큰 이동이 불가능한 경우, -1을 주어진 문제의 결과로 반환한다.

4. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 grid의 행과 열의 갯수를 저장한 변수이다.
- queue는 위치 별 소요 시간을 저장하기 위한 변수로, 오름차순으로 정렬하여 보관하기 위해 PriorityQueue로 정의하고 초기 값인 [0, 0, 0]을 넣어준다.
- visited는 방문한 위치를 저장하기 위한 변수로, $row \times col$ 크기의 2차원 부울 배열로 초기화하여 첫 위치인 visited[0][0] 위치를 true로 바꿔준다.

5. queue의 값이 존재할 때 까지 아래를 반복한다.
- curr에 queue의 첫 값을 꺼내 넣어주고, 위치를 저장할 x와 y에 curr[0], curr[1]의 값을 시간을 저장할 time에 curr[2]의 값을 넣어준다.
- DIRECTIONS의 각 값을 순차적으로 direction에 넣어 아래를 수행한다.
  - dx에 $x + direction[0]$을, dy에 $y + direction[1]$을 넣어준다.
  - dx와 dy가 grid 내 존재하면서 visited[dx][dy]가 false인 방문하지 않는 경우 아래를 계속 수행한다.
  - currTime에 $time + 1$인 현재 위치로 이동한 시간을 저장한다.
  - grid[dx][dy]의 값이 currTime보다 큰 경우, currTime에 이전 위치를 이동했다 돌아와서 시간을 소요하는 값인 $\frac{grid[dx][dy] - currTime + 1}{2} \times 2$를 더해준다.
  - queue에 [dx, dy, currTime]을 넣어준 후, visited[dx][dy]에 true를 넣어 방문하였음을 체크해준다.

6. 반복이 완료되면 마지막 위치까지 이동이 불가능하므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumTimeToVisitACellInAGrid.java){:target="_blank"}에서 확인 가능합니다.