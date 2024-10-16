---
title: "Leetcode Java Best Time to Buy and Sell Stock III"
excerpt: "Leetcode Best Time to Buy and Sell Stock III Java 풀이"
last_modified_at: 2021-08-13T12:00:00
header:
  image: /assets/images/leetcode/best-time-to-buy-and-sell-stock-iii.png
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
[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProfit(int[] prices) {
    int[] buy = new int[] { Integer.MAX_VALUE, Integer.MAX_VALUE };
    int[] sell = new int[2];
    for (int price : prices) {
      buy[0] = Math.min(buy[0], price);
      sell[0] = Math.max(sell[0], price - buy[0]);
      buy[1] = Math.min(buy[1], price - sell[0]);
      sell[1] = Math.max(sell[1], price - buy[1]);
    }
    return sell[1];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/537663413/){:target="_blank"}

# 설명
1. 주식에 대한 가격 정보를 담은 배열 prices를 이용하여 이익이 되는 값들 중 두 값의 합이 최대인 값을 구하는 문제이다.

2. 두 값의 합이 최대인 값을 구해야 하므로, 구매와 판매 가격을 저장할 buy와 sell을 크기 2의 정수 배열로 정의한다.

3. 주어진 배열 prices를 반복하여 두 값의 합이 최대인 구간을 찾는다.
- 첫 번째 구매 가격인 buy[0]는 buy[0]와 price 중 최소값으로 넣어준다.
- 첫 번째 판매 이익인 sell[0]는 sell[0]와 $price - buy[0]$ 중 최대값으로 넣어준다.
- 두 번째 구매 가격인 buy[1]은 buy[1]과 $price - sell[0]$ 중 최소값으로 넣어준다.
- 두 번째 판매 이익인 sell[1]은 sell[1]과 $price - buy[1]$ 중 최대값으로 넣어준다.
  - 두 번째 거래의 경우, 첫 번째 거래의 판매 이익을 두 번째 구매 비용에 통합하여 두 번째 판매 이익이 결국 두 판매 이익을 합친 결과가 되는 것이다.

4. 반복이 완료되면 두 판매 이익을 저장한 sell[1]을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BestTimeToBuyAndSellStockIII.java){:target="_blank"}에서 확인 가능합니다.