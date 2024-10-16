---
title: "Leetcode Java Magic Squares In Grid"
excerpt: "Leetcode Magic Squares In Grid Java"
last_modified_at: 2023-02-15T18:40:00
header:
  image: /assets/images/leetcode/magic-squares-in-grid.png
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
[Link](https://leetcode.com/problems/magic-squares-in-grid){:target="_blank"}

# 코드
```java
class Solution {

  public int numMagicSquaresInside(int[][] grid) {
    int result = 0;
    for (int i = 0; i <  grid.length - 2; i++) {
      for (int j = 0; j < grid[0].length - 2; j++) {
        if (this.isMagicSquare(grid, i, j)) {
          result++;
        }
      }
    }
    return result;
  }

  private boolean isMagicSquare(int[][] grid, int row, int col) {
    boolean[] visited = new boolean[10];
    for (int i = row; i < row + 3; i++) {
      for (int j = col; j < col + 3; j++) {
        if (grid[i][j] < 1 || grid[i][j] > 9 || visited[grid[i][j]]) {
          return false;
        }
        visited[grid[i][j]] = true;
      }
    }
    int sum = grid[row][col] + grid[row + 1][col + 1] + grid[row + 2][col + 2];
    if (sum != grid[row][col + 2] + grid[row + 1][col + 1] + grid[row + 2][col]) {
      return false;
    }
    for (int i = 0; i < 3; i++) {
      if (sum != grid[row + i][col] + grid[row + i][col + 1] + grid[row + i][col + 2] ||
          sum != grid[row][col + i] + grid[row + 1][col + i] + grid[row + 2][col + i]) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/magic-squares-in-grid/submissions/898391158/){:target="_blank"}

# 설명
1. grid 내에서 $3 \times 3$ 크기의 마법 사각형의 개수를 반환하는 문제이다.
- 마법 사각형은 [1, 9] 범위의 숫자들로 이루어진 $3 \times 3$ 크기의 사각형의 두 대각선과 세 행과, 열의 합이 모두 같은 사각형을 의미한다.

2. result는 마법 사각형의 개수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 grid의 길이보다 2 작은 값 미만까지 i를, 0부터 grid 첫 행의 길이보다 2 작은 값 미만까지 j를 증가시키며 아래를 수행한다.
- 4번에서 정의한 isMagicSquare(int[][] grid, int row, int col) 메서드를 수행한 결과가 true면 result를 증가시킨다.

4. 마법 사각형인지 검증하기 위한 isMagicSquare(int[][] grid, int row, int col) 메서드를 정의한다.
- visited는 각 숫자를 체크했는지 검증하기 위한 배열로, 크기가 10인 부울 배열로 초기화한다.
- row부터 우측 두 열까지, col부터 아래 두 행까지 [1, 9] 범위 내 값이면서 중복된 값이 있는지 검증하여 만족하지 않으면 false를 반환한다.
- sum에 대각선 하나의 합을 넣고 다른 대각선과 세 행, 열의 합이 모두 동일한지 검증하여 동일하지 않으면 false를, 동일하면 true를 반환한다.

5. 검증이 완료되면 마법 사각형의 개수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MagicSquaresInGrid.java){:target="_blank"}에서 확인 가능합니다.