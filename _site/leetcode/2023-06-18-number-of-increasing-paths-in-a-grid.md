---
title: "Leetcode Java Number of Increasing Paths in a Grid"
excerpt: "Leetcode Number of Increasing Paths in a Grid Java"
last_modified_at: 2023-06-18T09:40:00
header:
  image: /assets/images/leetcode/number-of-increasing-paths-in-a-grid.png
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
[Link](https://leetcode.com/problems/number-of-increasing-paths-in-a-grid){:target="_blank"}

# 코드
```java
class Solution {

  private int mod = 1000000007;
  private int[][] directions = new int[][] {
    { 1, 0 },
    { 0, -1 },
    { -1, 0 },
    { 0, 1 }
  };

  public int countPaths(int[][] grid) {
    int row = grid.length;
    int col = grid[0].length;
    int count = 0;
    int[][] dp = new int[row][col];
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        count = (count + this.getCount(grid, dp, row, col, i, j, 0)) % this.mod;
      }
    }
    return count;
  }

  private int getCount(int[][] grid, int[][] dp, int row, int col, int i, int j, int prev) {
    if (i < 0 || i >= row || j < 0 || j >= col || grid[i][j] <= prev) {
      return 0;
    } else if (dp[i][j] != 0) {
      return dp[i][j];
    } else {
      int count = 1;
      for (int[] direction : this.directions) {
        count = (count + this.getCount(grid, dp, row, col, i + direction[0], j + direction[1], grid[i][j])) % this.mod;
      }
      dp[i][j] = count;
      return count;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-increasing-paths-in-a-grid/submissions/973652653/){:target="_blank"}

# 설명
1. $m \times n$ 크기의 grid를 이용하여 임의의 위치에서 시작하고 종료하여 각 셀의 값이 점층적으로 증가하는 모든 경로의 수를 구하는 문제이다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- mod는 모듈러를 적용할 변수로, $10^9 +7$로 초기화한다.
- directions는 셀의 상하좌우를 계산하기 위한 배열로, 2차원 정수 배열로 초기화하여 상하좌우에 대한 x와 y축에 대한 가감값으로 이루어진 값들을 넣어준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 grid의 행과 열의 수를 저장한 변수이다.
- count는 시작과 종료가 점층적으로 증가하는 형태의 경로의 수를 계산하기 위한 변수로, 0으로 초기화한다.
- dp는 탐색 지점 별 경로의 수를 계산하기 위한 변수로, $row \times col$ 크기의 2차원 정수 배열로 초기화한다.

4. 0부터 row까지 i를, 0부터 col까지 j를 순차적으로 증가시키며 count에 count와 5번에서 정의한 getCount(int[][] grid, int[][] dp, int row, int col, int i, int j, int prev) 메서드를 수행한 결과를 더한 후 mod를 나눈 나머지 값을 넣어준다.

5. 이전 값이 prev인 위치에서 [i, j] 로 이동했을 때 증가하는 경로의 수를 계산하기 위한 getCount(int[][] grid, int[][] dp, int row, int col, int i, int j, int prev) 메서드를 정의한다.
- i가 [0, $row - 1$] j가 [0, $col - 1$] 범위를 벗어나거나 grid[i][j]의 값이 prev보다 같거나 작은 경우, 이어지는 경로가 없으므로 0을 반환한다.
- 위가 아니면서 dp[i][j]의 값이 0이 아닌 탐색된 경로의 경우, 해당 값을 반환한다.
- 위의 모든 경우가 아니라면 아래를 수행한다.
  - count는 경로를 계산할 변수로, 현재 위치까지 경로가 이어졌으므로 1을 넣어 초기화한다.
  - directions의 모든 값을 direction에 순차적으로 넣고 재귀 호출을 수행할 때 i, j, prev에 $i + direction[0]$, $j + direction[1]$, grid[i][j]의 값들을 순차적으로 수행한 결과에 count를 더한 후 mod를 나눈 나머지 값을 count에 더해준다.
- dp[i][j] 위치에 count를 넣어 저장한 후, count를 반환한다.

6. 반복이 완료되면 계산된 경로의 수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfIncreasingPathsInAGrid.java){:target="_blank"}에서 확인 가능합니다.