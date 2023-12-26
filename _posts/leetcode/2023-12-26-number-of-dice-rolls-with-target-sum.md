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

2. 경우의 수를 구하기 위한 3번의 numRollsToTarget(int[][] dp, int n, int k, int target) 메서드를 $(n + 1) \times (target + 1)$ 크기의 2차원 배열을 dp에 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

3. 재귀 호출을 통해 값을 구하기 위한 numRollsToTarget(int[][] dp, int n, int k, int target) 메서드를 정의한다.
- n과 target이 0인 경우, 1을 반환한다.
- target이 n 미만이거나 $n \times k$가 target 미만인 경우, 경우의 수가 없으므로 0을 반환한다.
- dp[n][target]의 값이 0이 아닌 경우, 이미 수행된 dp[n][target]의 값을 반환한다.
- 계산을 수행할 result를 0으로 초기화하고, 아래를 1부터 k까지 i를 증가시키며 반복한다.
  - target이 i보다 작은 경우, 반복을 중지한다.
  - result에 result와 n에 $n - 1$을, target에 $target - i$를 넣어 재귀 호출을 수행한 결과에 모둘러 $10^9 + 7$를 적용한 결과를 더한 값에 overflow를 방지하기 위해서 다시 모듈러 $10^9 + 7$를 적용한 값을 넣어준다.
- dp[n][target]에 저장된 result를 넣고 result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfDiceRollsWithTargetSum.java){:target="_blank"}에서 확인 가능합니다.