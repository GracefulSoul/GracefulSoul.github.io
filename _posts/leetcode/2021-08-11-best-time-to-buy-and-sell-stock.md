---
title: "Leetcode Java Best Time to Buy and Sell Stock"
excerpt: "Leetcode - 'Best Time to Buy and Sell Stock' 문제 Java 풀이"
last_modified_at: 2021-08-11T12:00:00
header:
  image: /assets/images/leetcode/best-time-to-buy-and-sell-stock.png
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
[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProfit(int[] prices) {
    int min = prices[0];
    int max = 0;
    for (int idx = 0; idx < prices.length; idx++) {
      if (prices[idx] < min) {
        min = prices[idx];
      }
      max = Math.max(max, prices[idx] - min);
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/536595288/){:target="_blank"}

# 설명
1. 주식에 대한 가격 정보를 담은 배열 prices를 이용하여 이익이 나올 수 있는 구간의 최대 금액을 찾는 문제이다.
- 단, 이득이 되는 구간이 없는 경우 0을 주어진 문제의 결과로 반환해야 한다.

2. 주어진 문제를 풀기 위한 변수를 정의한다.
- 변수 min을 주식의 저점(저가 지점)을 저장하기 위해 정의하여 prices의 첫 값으로 초기화 시킨다.
- 변수 max를 최대 이득이 되는 금액을 저장하기 위해 정의하여 0으로 초기화 시킨다.

3. 반복문을 이용하여 주어진 prices 배열을 순회하여 최대 이득이 되는 금액을 탐색한다.
- 만일 prices[idx]의 값이 min보다 작은 구간이면, min에 prices[idx] 값을 저장하여 최대 이익을 계속 탐색시킨다.
- 최대 이익을 저장하는 max에 현재 최대 이익인 max의 값과 $prices[idx] - min$의 값 중 큰 값을 저장하고 반복문을 계속 수행한다.

4. 반복이 완료되면 최대 이익을 저장한 변수 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BestTimeToBuyAndSellStock.java){:target="_blank"}에서 확인 가능합니다.