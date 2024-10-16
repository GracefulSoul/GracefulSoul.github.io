---
title: "Leetcode Java Path with Maximum Gold"
excerpt: "Leetcode Path with Maximum Gold Java"
last_modified_at: 2024-05-14T22:00:00
header:
  image: /assets/images/leetcode/path-with-maximum-gold.png
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
[Link](https://leetcode.com/problems/path-with-maximum-gold/){:target="_blank"}

# 코드
```java
class Solution {

  public int getMaximumGold(int[][] grid) {
    int row = grid.length;
    int col = grid[0].length;
    int result = 0;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        result = Math.max(result, this.getMaximumGold(grid, row, col, i, j, 0));
      }
    }
    return result;
  }

  private int getMaximumGold(int[][] grid, int row, int col, int i, int j, int sum) {
    if (grid[i][j] == 0) {
      return sum;
    } else {
      int max = 0;
      int curr = grid[i][j];
      grid[i][j] = 0;
      if (i > 0) {
        max = Math.max(max, this.getMaximumGold(grid, row, col, i - 1, j, sum));
      }
      if (i < row - 1) {
        max = Math.max(max, this.getMaximumGold(grid, row, col, i + 1, j, sum));
      }
      if (j > 0) {
        max = Math.max(max, this.getMaximumGold(grid, row, col, i, j - 1, sum));
      }
      if (j < col - 1) {
        max = Math.max(max, this.getMaximumGold(grid, row, col, i, j + 1, sum));
      }
      grid[i][j] = curr;
      max += curr;
      return max;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/path-with-maximum-gold/submissions/1257820418/){:target="_blank"}

# 설명
1. grid 내 아래 규칙에 따라 가장 많이 모을 수 있는 금의 갯수를 계산하는 문제이다.
- grid 내 셀의 값은 금의 갯수를 나타내며, 0인 경우 감옥을 의미한다.
- 현재 셀의 위치에서 상하좌우 네 방향 중 금이 존재하는 셀으로이동이 가능하며, 동일한 셀을 두 번 이상 방문할 수 없다.
- 금이 존재하는 임의 위치에서 금 수집을 중단할 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 grid의 행과 열의 수를 저장한 변수이다.
- result는 최대 금의 갯수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 row 미만까지 i를 증가시키며, 0부터 col 미만까지 j를 증가시키며 result에 result와 4번에서 정의한 getMaximumGold(int[][] grid, int row, int col, int i, int j, int sum) 메서드를 sum에 0을 넣어 수행한 결과를 넣어준다.

4. 상하좌우 네 방향을 재귀 호출을 통해 탐색하기 위한 getMaximumGold(int[][] grid, int row, int col, int i, int j, int sum) 메서드를 정의한다.
- grid[i][j]의 값이 0인 감옥인 경우, 현재까지 합산된 sum을 반환한다.
- 위의 경우가 아닌 금이 존재하는 셀이라면 아래를 수행한다.
  - max에 0을, curr에 grid[i][j]의 값인 현재 위치의 금의 갯수를 넣어준다.
  - grid[i][j]의 위치에 0을 넣어 현재 위치로 다시 돌아올 수 없도록 한다.
  - max에 max와 현재 위치에서 이동 가능한 상하좌우 네 방향으로 재귀 호출을 수행한 결과 중 가장 큰 값을 넣어준다.
  - grid[i][j]의 위치에 다시 curr을 넣어 값을 복원해준다.
  - max에 curr을 더해준 후 max를 반환해준다.

5. 3번의 반복이 완료되면 저장된 최대 금의 갯수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PathWithMaximumGold.java){:target="_blank"}에서 확인 가능합니다.