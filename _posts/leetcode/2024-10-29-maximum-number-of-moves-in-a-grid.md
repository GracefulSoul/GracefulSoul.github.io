---
title: "Leetcode Java Maximum Number of Moves in a Grid"
excerpt: "Leetcode - 'Maximum Number of Moves in a Grid' 문제 Java 풀이"
last_modified_at: 2024-10-29T19:40:00
header:
  image: /assets/images/leetcode/count-square-submatrices-with-all-ones.png
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
[Link](https://leetcode.com/problems/maximum-number-of-moves-in-a-grid/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxMoves(int[][] grid) {
    int row = grid.length;
    int col = grid[0].length;
    int[][] dp = new int[row][col];
    int result = 0;
    for (int j = col - 2; j >= 0; j--) {
      for (int i = 0; i < row; i++) {
        int num = grid[i][j];
        if (i - 1 >= 0 && grid[i - 1][j + 1] > num) {
          dp[i][j] = Math.max(dp[i][j], dp[i - 1][j + 1] + 1);
        }
        if (grid[i][j + 1] > num) {
          dp[i][j] = Math.max(dp[i][j], dp[i][j + 1] + 1);
        }
        if (row > i + 1 && grid[i + 1][j + 1] > num) {
          dp[i][j] = Math.max(dp[i][j], dp[i + 1][j + 1] + 1);
        }
      }
    }
    for (int i = 0; i < row; i++) {
      result = Math.max(result, dp[i][0]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-number-of-moves-in-a-grid/submissions/1437138646/){:target="_blank"}

# 설명
1. grid의 좌측 상단 위치에서 시작하여 오른쪽, 오른쪽 아래 대각선, 아래 중 현재 값보다 큰 위치로 이동할 수 있는 최대 횟수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 행과 열의 갯수를 저장한 변수이다.
- dp는 최대 이동 횟수를 계산하기 위한 배열로, $row \times col$ 크기의 2차원 정수 배열로 초기화한다.
- result는 최대 이동 횟수를 저장할 변수로, 0으로 초기화한다.

3. $col - 2$부터 0 이상까지 j를 감소시키고, 0부터 row 미만까지 i를 증가시키며 아래를 반복한다.
- num에 grid[i][j] 값을 넣어준다.
- $i - 1$이 0 이상이면서 grid[$i - 1$][$j + 1$]이 num보다 커 해당 위치로 이동 가능한 경우, dp[i][j]의 위치에 해당 값과 dp[$i - 1$][$j + 1$]의 값에 1을 더한 값 중 큰 값을 넣어준다.
- grid[i][$j + 1$]의 값이 num보다 커 해당 위치로 이동 가능한 경우, dp[i][j]의 위치에 해당 값과 grid[i][$j + 1$]의 값에 1을 더한 값 중 큰 값을 넣어준다.
- row가 $i + 1$보다 크고 grid[$i + 1$][$j + 1$]의 값이 num보다 커 해당 위치로 이동 가능한 경우, dp[i][j]의 위치에 해당 값과 grid[$i + 1$][$j + 1$]의 값에 1을 더한 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 dp의 이동 횟수가 저장된 각 행의 첫 열 중 큰 값을 result에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumNumberOfMovesInAGrid.java){:target="_blank"}에서 확인 가능합니다.