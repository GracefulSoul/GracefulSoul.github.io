---
title: "Leetcode Java Coin Change 2"
excerpt: "Leetcode Coin Change 2 Java"
last_modified_at: 2022-06-04T11:00:00
header:
  image: /assets/images/leetcode/coin-change-2.png
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
[Link](https://leetcode.com/problems/coin-change-2/){:target="_blank"}

# 코드
```java
class Solution {

  public int change(int amount, int[] coins) {
    int[] dp = new int[amount + 1];
    dp[0] = 1;
    for (int coin : coins) {
      for (int idx = coin; idx <= amount; idx++) {
        dp[idx] += dp[idx - coin];
      }
    }
    return dp[amount];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/713881945/){:target="_blank"}

# 설명
1. [Coin Change](../coin-change){:target="_blank"}와 유사한 문제로, coins 내 각 coin을 활용하여 amount의 금액이 되는 경우의 수를 구하는 문제이다.
- 단, 각 coin은 반복 사용이 가능하다.

2. dp는 각 경우의 수를 구하기 위한 배열로, $amount + 1$ 크기로 정의하고 첫 값에 1을 넣어준다.

3. coins의 모든 값을 반복하고, coin부터 amount 이하까지 idx를 증가시키며 반복을 하여 아래를 수행한다.
- dp의 idx번째 경우의 수에 dp의 $idx - coin$번째 경우의 수를 더하여 dp의 idx번째 위치의 값이 amount일 경우 만들 수 있는 경우의 수를 추가해준다.

4. 반복이 완료되어 dp에 값이 다 들어가면 주어진 문제의 결과로 dp의 amount번째 값을 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CoinChange2.java){:target="_blank"}에서 확인 가능합니다.