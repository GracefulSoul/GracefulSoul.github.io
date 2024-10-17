---
title: "Leetcode Java Unique Paths II"
excerpt: "Leetcode - 'Unique Paths II' 문제 Java 풀이"
last_modified_at: 2021-06-14T15:00:00
header:
  image: /assets/images/leetcode/unique-paths-ii.png
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
[Link](https://leetcode.com/problems/unique-paths-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int uniquePathsWithObstacles(int[][] obstacleGrid) {
    int[][] dp = new int[obstacleGrid.length + 1][obstacleGrid[0].length + 1];
    dp[1][1] = obstacleGrid[0][0] != 1 ? 1 : 0;
    for (int i = 1; i < dp.length; i++) {
      for (int j = 1; j < dp[0].length; j++) {
        dp[i][j] += obstacleGrid[i - 1][j - 1] != 1 ? dp[i][j - 1] + dp[i - 1][j] : 0;
      }
    }
    return dp[obstacleGrid.length][obstacleGrid[0].length];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/507663085/){:target="_blank"}

# 설명
1. 기존 풀이한 [Unique Paths](../unique-paths/)와 비슷한 문제로, 시작점에서 출발하여 정해진 포인트를 거쳐 도착점까지 도달하는 경우의 수를 구하는 문제이다.

2. 경우의 수를 구하기 위해 DP를 주어진 배열 obstacleGrid의 크기보다 한 사이즈 크게 정의한다.

3. 초기 값인 db[1][1]은 obstacleGrid[0][0]의 값이 경유지인 1인 경우에는 0으로, 경유지가 아닌 경우 1로 설정한다.

4. dp를 반복하여 경유지를 거쳐 도착점까지 도달하는 경우의 수를 구한다.
- dp[i][j]에 obstacleGrid[$i - 1$][$j - 1$]의 값이 경유지인 1인 경우 0을, 1이 아닌 경우 dp[i][$j - 1]의 값과 dp[$i - 1$][j]의 값을 합하여 넣어준다.

5. 반복이 완료되면 경유지를 거쳐 도착지에 도달하기까지의 경우의 수인 dp[obstacleGrid.length][obstacleGrid[0].length]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniquePathsII.java){:target="_blank"}에서 확인 가능합니다.