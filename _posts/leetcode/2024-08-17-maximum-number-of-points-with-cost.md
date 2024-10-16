---
title: "Leetcode Java Maximum Number of Points with Cost"
excerpt: "Leetcode Maximum Number of Points with Cost Java"
last_modified_at: 2024-08-17T10:00:00
header:
  image: /assets/images/leetcode/maximum-number-of-points-with-cost.png
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
[Link](https://leetcode.com/problems/maximum-number-of-points-with-cost/){:target="_blank"}

# 코드
```java
class Solution {

  public long maxPoints(int[][] points) {
    int row = points.length;
    int col = points[0].length;
    long[] dp = new long[col];
    long result = 0;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        dp[j] += points[i][j];
      }
      for (int j = 1; j < col; j++) {
        dp[j] = Math.max(dp[j], dp[j - 1] - 1);
      }
      for (int j = col - 2; j >= 0; j--) {
        dp[j] = Math.max(dp[j], dp[j + 1] - 1);
      }
    }
    for (int i = 0; i < col; i++) {
      result = Math.max(result, dp[i]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-number-of-points-with-cost/submissions/1358369378/){:target="_blank"}

# 설명
1. $m \times n$ 크기의 points의 각 행의 점수 중 하나를 골라 달성할 수 있는 최대 점수를 계산하는 문제이다.
- 단, 앞 열에서 너무 떨어진 열의 점수를 선택하면 점수를 잃게된다.
- $0 <= r < m - 1$을 만족하는 r과 $r + 1$의 인접한 행 에서 (r, c<sub>1</sub>), ($r + 1$, c<sub>2</sub>)에서 셀을 선택하는 경우, $abs(c1 - c2)$의 값을 차감한다.
- abs(x)는 x >= 0인 경우 x를, x < 0인 경우 -x를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 points의 행과 열의 수를 저장한 변수이다.
- dp는 점수 계산을 위한 변수로, long형의 col 크기 정수 배열로 초기화한다.
- result는 점수 계산을 위한 변수로, 0으로 초기화한다.

3. 0부터 row 미만일 때 까지 i를 증가시키며 아래를 반복한다.
- 0부터 col 미만까지 j를 증가시키며, dp[j]에 points[i][j]를 더해 기본 점수를 넣어준다.
- 1부터 col 미만까지 j를 증가시키며, dp[j]에 현재 값과 $dp[j - 1] - 1$ 중 큰 값인 최대 점수를 넣어준다.
- $col - 2$부터 0 이상일 때 까지 j를 감소시키며, dp[j]에 현재 값과 $dp[j + 1] - 1$ 중 큰 값인 최대 점수를 넣어준다.

4. 위의 반복으로 계산된 dp 내 최대 점수를 result에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumNumberOfPointsWithCost.java){:target="_blank"}에서 확인 가능합니다.