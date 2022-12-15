---
title: "Leetcode Java Largest Plus Sign"
excerpt: "Leetcode Largest Plus Sign Java"
last_modified_at: 2022-12-15T11:30:00
header:
  image: /assets/images/leetcode/largest-plus-sign.png
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
[Link](https://leetcode.com/problems/largest-plus-sign){:target="_blank"}

# 코드
```java
class Solution {

  public int orderOfLargestPlusSign(int n, int[][] mines) {
    int[][] grid = new int[n][n];
    for (int[] row : grid) {
      Arrays.fill(row, n);
    }
    for (int[] mine : mines) {
      grid[mine[0]][mine[1]] = 0;
    }
    for (int i = 0; i < n; i++) {
      int[] direction = new int[] { 0, 0, 0, 0 };
      for (int j = 0, k = n - 1; j < n; j++, k--) {
        grid[i][j] = Math.min(grid[i][j], direction[0] = (grid[i][j] == 0 ? 0 : direction[0] + 1));
        grid[i][k] = Math.min(grid[i][k], direction[1] = (grid[i][k] == 0 ? 0 : direction[1] + 1));
        grid[j][i] = Math.min(grid[j][i], direction[2] = (grid[j][i] == 0 ? 0 : direction[2] + 1));
        grid[k][i] = Math.min(grid[k][i], direction[3] = (grid[k][i] == 0 ? 0 : direction[3] + 1));
      }
    }
    int result = 0;
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
        result = Math.max(result, grid[i][j]);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-plus-sign/submissions/859948375/){:target="_blank"}

# 설명
1. $n \times n$ 크기의 배열 내 지뢰의 좌표인 mines를 피해서 만들 수 있는 상하좌우의 길이가 동일한 '+' 기호의 중심으로부터 최대 길이를 구하는 문제이다.
- 배열 내 빈 칸은 1로, 지뢰는 0으로 표기한다.

2. grid는 주어진 배열을 구성하기 위한 변수로, $n \times n$ 크기로 초기화 하고 아래를 수행한다.
- grid의 모든 값에 임의 큰 숫자인 n을 넣어준다.
- grid 내 mines의 모든 위치에 0을 넣어준다.

3. 0부터 n까지 i를 증가시키며 direction 배열을 좌, 우, 상, 하 순으로 0으로 초기화시키고 아래를 반복한다.
- j는 0부터 n 미만까지 증가시키고, k는 $n - 1$부터 감소시키며 아래를 반복하여 사방면으로 검증을 수행한다.
  - grid[i][j]의 값에 해당 값과 grid[i][j]의 값이 0인 지뢰인 값인지 검증하여 지뢰의 경우 direction[0]을 0으로 초기화시키고, 아니면 direction[0]을 증가시킨 값 중 작은 값을 넣어 위에서 우측으로 최대 길이 계산을 수행한다.
  - grid[i][k]의 값에 해당 값과 grid[i][k]의 값이 0인 지뢰인 값인지 검증하여 지뢰의 경우 direction[1]을 0으로 초기화시키고, 아니면 direction[1]을 증가시킨 값 중 작은 값을 넣어 위에서 좌측으로 최대 길이 계산을 수행한다.
  - grid[j][i]의 값에 해당 값과 grid[j][i]의 값이 0인 지뢰인 값인지 검증하여 지뢰의 경우 direction[2]을 0으로 초기화시키고, 아니면 direction[2]을 증가시킨 값 중 작은 값을 넣어 좌측에서 아래로 최대 길이 계산을 수행한다.
  - grid[k][i]의 값에 해당 값과 grid[k][i]의 값이 0인 지뢰인 값인지 검증하여 지뢰의 경우 direction[3]을 0으로 초기화시키고, 아니면 direction[3]을 증가시킨 값 중 작은 값을 넣어 우측에서 위로 최대 길이 계산을 수행한다.

4. 결과를 넣어줄 result에 grid 내 모든 값 중 최댓 값인 '+' 기호의 중심으로부터 최대 길이를 넣어준다.

5. 4번을 통해 찾은 최대 길이인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestPlusSign.java){:target="_blank"}에서 확인 가능합니다.