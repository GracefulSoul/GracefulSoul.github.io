---
title: "Leetcode Java Best Time to Buy and Sell Stock with Transaction Fee"
excerpt: "Leetcode Best Time to Buy and Sell Stock with Transaction Fee Java"
last_modified_at: 2022-11-04T10:00:00
header:
  image: /assets/images/leetcode/best-time-to-buy-and-sell-stock-with-transaction-fee.png
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
[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProfit(int[] prices, int fee) {
    int profit = 0;
    int hold = -prices[0];
    for (int price : prices) {
      profit = Math.max(profit, hold + price - fee);
      hold = Math.max(hold, profit - price);
    }
    return profit;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/836420002/){:target="_blank"}

# 설명
1. 동일 주식의 가격을 넣은 배열인 prices를 이용하여 거래 수수료가 fee인 거래를 통해 최대 이익을 찾는 문제이다.
- 단, 주식을 구매하면 반드시 판매 후 구매해야한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- profit은 최대 이익을 넣을 변수로, 0으로 초기화한다.
- hold는 판매하지 않고 유지할 경우의 금액으로, prices의 첫 값을 음수로 전환한 임의 값을 넣어준다.

3. prices의 모든 값을 price에 넣어 아래를 반복 수행한다.
- profit에 기존 이익 금액인 profit과 구매했을 때의 값인 $hold + price - fee$ 중 큰 값을 넣어준다.
- hold에 기존 유지 금액인 hold와 판매했을 때의 값인 $profit - price$ 중 큰 값을 넣어준다.

4. 반복이 완료되면 최대 이익을 저장한 profit을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BestTimeToBuyAndSellStockWithTransactionFee.java){:target="_blank"}에서 확인 가능합니다.