---
title: "Leetcode Java Number of Dice Rolls With Target Sum"
excerpt: "Leetcode Number of Dice Rolls With Target Sum Java"
last_modified_at: 2023-12-26T11:45:00
header:
  image: /assets/images/leetcode/number-of-dice-rolls-with-target-sum.png
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
[Link](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum){:target="_blank"}

# 코드
```java
class Solution {

  public int numRollsToTarget(int n, int k, int target) {
    return this.numRollsToTarget(new int[n + 1][target + 1], n, k, target);
  }

  private int numRollsToTarget(int[][] dp, int n, int k, int target) {
    if (n == 0 && target == 0) {
      return 1;
    }
    if (target < n || n * k < target) {
      return 0;
    }
    if (dp[n][target] != 0) {
      return dp[n][target];
    }
    int result = 0;
    for (int i = 1; i <= k; i++) {
      if (target < i) {
        break;
      }
      result = (result + this.numRollsToTarget(dp, n - 1, k, target - i) % 1000000007) % 1000000007;
    }
    dp[n][target] = result;
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/submissions/1128529662/){:target="_blank"}

# 설명
1. [1, k] 범위의 k면의 주사위를 n번 돌려서 target이 되는 경우의 수를 구하는 문제이다.
- 단, 값이 매우 클 수 있으므로 모듈러 $10^9 + 7$를 적용한다.

2. 

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfDiceRollsWithTargetSum.java){:target="_blank"}에서 확인 가능합니다.