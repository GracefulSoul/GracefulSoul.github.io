---
title: "Leetcode Java Best Time to Buy and Sell Stock IV"
excerpt: "Leetcode - 'Best Time to Buy and Sell Stock IV' 문제 Java 풀이"
last_modified_at: 2021-09-28T13:00:00
header:
  image: /assets/images/leetcode/best-time-to-buy-and-sell-stock-iv.png
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
[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProfit(int k, int[] prices) {
    int length = prices.length;
    if (k >= length / 2) {
      return this.getMaxProfit(prices, length);
    } else {
      return this.getMaxProfitUsingDp(k, prices, length);
    }
  }

  private int getMaxProfit(int[] prices, int length) {
    int max = 0;
    for (int idx = 1; idx < length; idx++) {
      if (prices[idx] > prices[idx - 1]) {
        max += prices[idx] - prices[idx - 1];
      }
    }
    return max;
  }

  private int getMaxProfitUsingDp(int k, int[] prices, int length) {
    int[][] dp = new int[k + 1][length];
    for (int i = 1; i <= k; i++) {
      int max = dp[i - 1][0] - prices[0];
      for (int j = 1; j < length; j++) {
        dp[i][j] = Math.max(dp[i][j - 1], prices[j] + max);
        max = Math.max(max, dp[i - 1][j] - prices[j]);
      }
    }
    return dp[k][length - 1];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/562177464/){:target="_blank"}

# 설명
1. 주어진 배열인 prices는 주식 가격으로, 주어진 정수인 k번 까지 거래를 통해 발생 할 수 있는 최대 이익을 구하는 문제이다.

2. 주어진 배열인 prices 크기의 절반보다 k가 크거나 같을 경우 3번을, k가 작을 경우 4번을 수행한다.

3. 매매와 매도의 횟수가 최대 거래 횟수인 k를 넘지 못하기 때문에 직전 값의 차이로만 계산해도 최대 이익을 구할 수 있으므로 반복문을 통해 최대 이익을 계산한다.
- 최대 이익을 저장할 변수 max를 정의한다.
- 두 번째 값인 1부터 주어진 배열 prices의 크기인 length 전까지 반복하여 다음 주식의 가격이 높을 경우, max에 해당 차이 값을 더해준다.
- 반복이 완료되면, 주어진 배열인 prices를 이용하여 최대 k번 거래 후 최대 이익이 되는 max를 주어진 문제의 결과로 반환한다.

4. 매매와 매도의 횟수가 최대 거래 횟수인 k번의 각 경우를 따져야 하기 때문에, DP를 이용하여 k번 거래 동안 발생 가능한 최대 이익을 계산한다.
- DP를 활용하기 위한 배열 dp를 [$k + 1$][length]의 크기로 정의한다.
- 최소 거래 횟수인 1부터 최대 거래 횟수인 k번까지 반복하여 DP를 초기화한다.
- 각 거래 횟수에 따라 최대 이익을 저장할 max를 dp[$i - 1$][0]의 값과 prices[0]의 값 차이를 넣어준다.
- prices 배열을 탐색하여 dp에 최대 이익을 넣어준다.
- dp[i][j]에 이전 값인 dp[i][$j - 1$]의 값과 $prices[j] + max$의 값 중 큰 값을 넣어준다.
- max에 max와 동일 prices 배열의 값 위치에 직전 거래 횟수의 이익 중 큰 값을 넣어 횟수와 무관한 최대 이익을 max에 저장시키고 반복을 계속 수행한다.
- 모든 반복이 완료되어 dp의 값이 채워지면, 주어진 배열인 prices를 이용하여 최대 k번 거래 후 최대 이익이 되는 dp[k][length - 1]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BestTimeToBuyAndSellStockIV.java){:target="_blank"}에서 확인 가능합니다.