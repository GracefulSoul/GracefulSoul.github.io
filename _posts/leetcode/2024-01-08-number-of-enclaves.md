---
title: "Leetcode Java Number of Enclaves"
excerpt: "Leetcode Number of Enclaves Java"
last_modified_at: 2024-01-08T11:20:00
header:
  image: /assets/images/leetcode/number-of-enclaves.png
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
[Link](https://leetcode.com/problems/number-of-enclaves){:target="_blank"}

# 코드
```java
class Solution {

  public int numEnclaves(int[][] grid) {
    int row = grid.length;
    int col = grid[0].length;
    int result = 0;
    for (int i = 0; i < row; i++) {
      this.dfs(grid, i, 0);
      this.dfs(grid, i, col - 1);
    }
    for (int j = 0; j < col; j++) {
      this.dfs(grid, 0, j);
      this.dfs(grid, row - 1, j);
    }
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (grid[i][j] == 1) {
          result++;
        }
      }
    }
    return result;
  }

  private void dfs(int grid[][], int i, int j) {
    if (0 <= i && i <= grid.length - 1 && 0 <= j && j <= grid[i].length - 1 && grid[i][j] == 1) {
      grid[i][j] = 0;
      this.dfs(grid, i + 1, j);
      this.dfs(grid, i - 1, j);
      this.dfs(grid, i, j + 1);
      this.dfs(grid, i, j - 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-enclaves/submissions/1140028386/){:target="_blank"}

# 설명
1. grid 내 육지와 인접하지 않은 섬의 크기를 반환하는 문제이다.
- grid의 가장자리는 육지와 인접해있다.
- '0'은 바다를, '1'은 육지를 의미한다.

2. 재귀 호출을 이용하여 육지와 인접한 셀을 바다로 바꾸어줄 dfs(int grid[][], int i, int j) 메서드를 정의한다.
- i와 j가 grid 내 범위에 있으면서 grid[i][j]가 1인 육지인 경우 아래를 수행한다.
  - grid[i][j]의 위치에 0을 넣어 바다로 바꾸어준다.
  - 상하좌우를 반복하여 인접한 육지를 모두 바다로 바꾸어준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 행과 열의 길이를 저장한 변수이다.
- result는 육지와 인접하지 않은 섬의 크기를 저장할 변수로, 0으로 초기화한다.

4. 0부터 row 미만까지 i를 증가시키며 행의 시작과 종료 위치에 인접한 육지를 2번에서 정의한 dfs(int grid[][], int i, int j) 메서드를 수행하여 제거해준다.

5. 0부터 col 미만까지 j를 증가시키며 열의 시작과 종료 위치에 인접한 육지를 2번에서 정의한 dfs(int grid[][], int i, int j) 메서드를 수행하여 제거해준다.

6. grid 내 셀의 값이 1인 육지인 경우 result를 증가시켜 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfEnclaves.java){:target="_blank"}에서 확인 가능합니다.