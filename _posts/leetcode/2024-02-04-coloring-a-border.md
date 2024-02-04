---
title: "Leetcode Java Coloring A Border"
excerpt: "Leetcode Coloring A Border Java"
last_modified_at: 2024-02-04T10:10:00
header:
  image: /assets/images/leetcode/coloring-a-border.png
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
[Link](https://leetcode.com/problems/coloring-a-border){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] colorBorder(int[][] grid, int row, int col, int color) {
    int rows = grid.length;
    int cols = grid[0].length;
    if (grid[row][col] != color) {
      this.dfs(grid, row, col, color, grid[row][col], new boolean[rows][cols], rows, cols);
    }
    return grid;
  }

  private void dfs(int[][] grid, int row, int col, int color, int value, boolean[][] visited, int rows, int cols) {
    if (row < 0 || rows <= row || col < 0 || cols <= col || grid[row][col] != value || visited[row][col]) {
      return;
    }
    visited[row][col] = true;
    boolean border = false;
    if (row == 0 || col == 0 || col == cols - 1 || row == rows - 1 || grid[row + 1][col] != value
        || grid[row - 1][col] != value || grid[row][col - 1] != value || grid[row][col + 1] != value) {
      border = true;
    }
    this.dfs(grid, row + 1, col, color, value, visited, rows, cols);
    this.dfs(grid, row - 1, col, color, value, visited, rows, cols);
    this.dfs(grid, row, col + 1, color, value, visited, rows, cols);
    this.dfs(grid, row, col - 1, color, value, visited, rows, cols);
    if (border) {
      grid[row][col] = color;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/coloring-a-border/submissions/1165340389/){:target="_blank"}

# 설명
1. grid[row][col] 위치에서 시작하여 아래의 조건을 만족하는 셀들에 color의 값을 넣어 반환하는 문제이다.
- grid[row][col] 값과 인접한 네 방향의 셀의 값이 다른 경우 grid의 경계라 칭한다.
- grid의 경계에 해당하는 값들을 모두 color를 넣어준다.

2. rows와 cols에 grid의 행과 열의 길이를 저장해서 넣어준다.

3. grid[row][col]이 color를 만족하지 않는 경우, 4번에서 정의한 dfs(int[][] grid, int row, int col, int color, int value, boolean[][] visited, int rows, int cols) 메서드를 value에 grid[row][col] 값과 visited에 $rows \times cols$ 크기의 2차원 부울 배열을 넣어 수행한다.

4. DFS 방식으로 grid에 color를 색칠할 dfs(int[][] grid, int row, int col, int color, int value, boolean[][] visited, int rows, int cols) 메서드를 정의한다.
- 아래의 조건을 만족하면 색을 칠할 수 없으므로, 수행을 종료한다.
  - row와 col이 grid의 범위를 벗어나는 경우.
  - grid[row][col] 값이 value가 아닌 경우.
  - visited[row][col] 값이 true인 이미 방문한 셀인 경우.
- visited[row][col]의 값을 true로 바꾼 후, border인지 검증하기 위한 값을 false로 초기화한다.
- row과 col가 범위를 벗어나거나 상하좌우의 값이 value가 아닌 경우, border를 만족하므로 true로 바꾸어준다.
- grid[row][col] 위치에서 네 방향을 순차적으로 재귀 호출을 수행해준다.
- border가 true이면 색을 칠할 수 있으므로, gird[row][col]의 위치에 color를 넣어준다.

5. 결과가 저장된 grid를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ColoringABorder.java){:target="_blank"}에서 확인 가능합니다.