---
title: "Leetcode Java Coin Change"
excerpt: "Leetcode - 'Coin Change' 문제 Java 풀이"
last_modified_at: 2021-12-31T13:00:00
header:
  image: /assets/images/leetcode/coin-change.png
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
[Link](https://leetcode.com/problems/coin-change/){:target="_blank"}

# 코드
```java
class Solution {

  public int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1);
    dp[0] = 0;
    for (int idx = 0; idx < amount + 1; idx++) {
      for (int coin : coins) {
        if (idx >= coin) {
          dp[idx] = Math.min(dp[idx], 1 + dp[idx - coin]);
        }
      }
    }
    return dp[amount] > amount ? -1 : dp[amount];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/610175098/){:target="_blank"}

# 설명
1. 주어진 정수 배열 coins의 값들로 amount를 만들 수 있는 최소한의 코인의 개수를 구하는 문제이다.
- 단, amount를 만들 수 없는 경우 -1을 주어진 문제의 결과로 반환한다.

2. dp 배열을 $amount + 1$ 크기로 정의하고, 첫 값에는 0을 그 외에는 amount + 1 값을 넣어준다.

3. 0부터 $amount + 1$까지 idx를 증가시키며 dp에 값을 넣어준다.
- coins를 반복하여 idx가 coin의 값보다 큰 경우, dp의 idx번째 값에 dp의 idx번째 값과 dp의 $idx - coin$의 값에 1을 더한 값보다 작은 값을 넣어준다.

4. 반복이 완료되어 dp에 값이 다 채워진 경우, dp의 amount번쨰 값이 amount보다 큰 경우 -1을 작은 경우 dp의 amount번째 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CoinChange.java){:target="_blank"}에서 확인 가능합니다.