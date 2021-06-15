---
title: "Leetcode Java Minimum Path Sum"
excerpt: "Leetcode Minimum Path Sum Java 풀이"
last_modified_at: 2021-06-15T12:30:00
header:
  image: /assets/images/leetcode/minimum-path-sum.png
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
[Link](https://leetcode.com/problems/minimum-path-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public int minPathSum(int[][] grid) {
    int[] dp = this.getDp(grid);
    for (int i = 1; i < grid.length; i++) {
      for (int j = 0; j < grid[i].length; j++) {
        if (j == 0) {
          dp[j] += grid[i][j];
        } else {
          dp[j] = grid[i][j] + Math.min(dp[j - 1], dp[j]);
        }
      }
    }
    return dp[grid[0].length - 1];
  }

  public int[] getDp(int[][] grid) {
    int[] dp = new int[grid[0].length];
    dp[0] = grid[0][0];
    for (int j = 1; j < grid[0].length; j++) {
      dp[j] = dp[j - 1] + grid[0][j];
    }
    return dp;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/508070444/){:target="_blank"}

# 설명
1. 좌측 상단에서 시작해서 우측 하단으로 이동하기까지 배열 내 값의 합이 낮은 값을 탐색하는 문제이다.

2. 누적 합을 구하기 위해 DP를 주어진 2차원 배열 grid의 열 길이만큼 정의한다.
- 각 이동 간 합을 순차적으로 보기 위해서는 grid와 동일 크기로 정의해도 되나, 최소 이동 횟수만 구하면 되므로 grid의 열 길이만큼 정의하여 이동 값의 합을 구한다.

3. 정의한 DP에 첫 행을 반복하여 순차적으로 누계를 저장한다.

4. 주어진 2차원 배열 grid를 반복하여 우측 하단 마지막 셀에 도달하기 까지 최소 합을 구한다.
- DP를 주어진 배열 grid의 첫 행으로 초기화 하였으므로, 다음 행부터 반복을 수행한다.
- 첫 열의 경우, DP의 같은 열에 배열의 값을 누적시킨다.
  - 점진적으로 우측 하단으로 이동하므로, 첫 열은 하단으로 이동하는 경우로 판단한다.
- 그 외의 경우, DP의 같은 열에 배열의 값과 DP[$j - 1$]과 DP[j]의 값 중 작은 값을 더한다.
  - 우측 하단으로 점진적으로 이동하면서 바로 아래칸으로 이동하는 경우와, 옆칸으로 이동하는 경우의 최소 값을 더하여 목적지에 도착하기 위한 최소 합을 구한다.

5. 반복이 완료되면, DP의 마지막 열 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumPathSum.java){:target="_blank"}에서 확인 가능합니다.