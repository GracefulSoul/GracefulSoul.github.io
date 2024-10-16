---
title: "Leetcode Java Best Time to Buy and Sell Stock II"
excerpt: "Leetcode Best Time to Buy and Sell Stock II Java 풀이"
last_modified_at: 2021-08-12T12:00:00
header:
  image: /assets/images/leetcode/best-time-to-buy-and-sell-stock-ii.png
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
[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProfit(int[] prices) {
    int idx = 0;
    int sum = 0;
    int min = 0;
    while (idx < prices.length) {
      while (idx < prices.length - 1 && prices[idx] >= prices[idx + 1]) {
        idx++;
      }
      min = prices[idx++];
      while (idx < prices.length - 1 && prices[idx] <= prices[idx + 1]) {
        idx++;
      }
      sum += prices.length > idx ? prices[idx++] - min : 0;
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/537161438/){:target="_blank"}

# 설명
1. 주식에 대한 가격 정보를 담은 배열 prices를 이용하여 이익이 되는 값들의 합이 최대인 결과를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- idx는 이익을 발생시킬 수 있는 최소와 최대 index를 구하기 위한 임시 변수이다.
- sum은 각 이익들의 합을 저장하기 위한 변수이다.
- min은 이익을 발생시킬 수 있는 최소 index의 값을 임시 저장하기 위한 변수이다.

3. 주어진 배열 prices를 반복하여 최대 이익의 합을 구한다.
- 반복을 통해 idx가 $prices.length - 1$보다 작고 현재의 값이 다음 값보다 크거나 같을 경우, idx를 증가시킨다.
- 위에서 증가된 idx의 위치는 최소한의 이익 실현이 가능한 시작 위치이므로, min에 prices[idx] 값을 저장하고 idx를 증가시킨다.
- 반복을 통해 idx가 $prices.length - 1$보다 작고 현재의 값이 다음 값보다 작거나 같을 경우, idx를 증가시킨다.
- 위에서 증가된 idx의 위치는 이익 실현이 가능한 위치이거나 prices의 크기를 벗어난 경우이므로, prices의 길이보다 idx가 작으면 sum에 $prices[idx] - min$을 더한다.

4. 반복이 완료되면 최대 이익의 합을 저장한 변수 sum을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BestTimeToBuyAndSellStockII.java){:target="_blank"}에서 확인 가능합니다.