---
title: "Leetcode Java Number of Closed Islands"
excerpt: "Leetcode - 'Number of Closed Islands' 문제 Java 풀이"
last_modified_at: 2025-04-12T23:10:00
header:
  image: /assets/images/leetcode/number-of-closed-islands.png
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
[Link](https://leetcode.com/problems/number-of-closed-islands/){:target="_blank"}

# 코드
```java
class Solution {

  public int closedIsland(int[][] grid) {
    int row = grid.length;
    int col = grid[0].length;
    int result = 0;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (grid[i][j] == 0 && this.dfs(grid, row, col, i, j)) {
          result++;
        }
      }
    }
    return result;
  }

  private boolean dfs(int[][] grid, int row, int col, int i, int j) {
    if (i < 0 || row <= i || j < 0 || col <= j) {
      return false;
    } else if (grid[i][j] == 1) {
      return true;
    } else {
      grid[i][j] = 1;
      boolean left = this.dfs(grid, row, col, i, j - 1);
      boolean top = this.dfs(grid, row, col, i - 1, j);
      boolean right = this.dfs(grid, row, col, i, j + 1);
      boolean bottom = this.dfs(grid, row, col, i + 1, j);
      return left && right && top && bottom;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-closed-islands/submissions/1604573858/){:target="_blank"}

# 설명
1. 0은 땅, 1은 물을 나타내는 값들로 이루어진 grid를 이용하여 물 사이에 존재하는 섬의 갯수를 계산하는 문제이다.

2. 물 사이에 존재하는 섬을 검증하기 위한 dfs(int[][] grid, int row, int col, int i, int j) 메서드를 정의한다.
- i가 [0, $row - 1$], j가 [0, $col - 1$] 범위를 벗어나는 경우, false를 반환한다.
- grid[i][j]의 값이 1인 물인 경계에 도달하는 경우, true를 반환한다.
- 그 외의 경우 아래를 수행한다.
  - gird[i][j]의 값을 1로 바꾸어 방문한 위치임을 저장한다.
  - 주어진 조건 순서대로 left, top, right, bottom 위치 별 재귀 호출을 수행한 결과가 모두 true인 물 사이에 존재하는 섬인지 검증한 결과를 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 grid의 행과 열의 갯수를 저장한 변수이다.
- result는 섬의 갯수를 저장하기 위한 변수로, 0으로 초기화한다.

4. 0부터 row 미만까지 i를, 0부터 col 미만까지 j를 증가시키며 아래를 반복한다.
- grid[i][j]가 육지이면서 2번에서 정의한 dfs(int[][] grid, int row, int col, int i, int j) 메서드를 수행한 결과가 true인 조건을 만족하는 경우, result를 증가시켜준다.

5. 반복이 완료되면 물 사이에 존재하는 섬의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfClosedIslands.java){:target="_blank"}에서 확인 가능합니다.