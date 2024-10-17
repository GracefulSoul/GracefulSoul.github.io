---
title: "Leetcode Java Best Time to Buy and Sell Stock with Cooldown"
excerpt: "Leetcode - 'Best Time to Buy and Sell Stock with Cooldown' 문제 Java 풀이"
last_modified_at: 2021-12-20T13:00:00
header:
  image: /assets/images/leetcode/best-time-to-buy-and-sell-stock-with-cooldown.png
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
[Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProfit(int[] prices) {
    int sold = 0;
    int hold = Integer.MIN_VALUE;
    int rest = 0;
    for (int price : prices) {
      hold = Math.max(hold, rest - price);
      rest = Math.max(rest, sold);
      sold = hold + price;
    }
    return Math.max(sold, rest);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/604340980/){:target="_blank"}

# 설명
1. 주어진 정수 배열 prices를 이용하여 최대 이익을 낼 수 있는 금액을 구하는 문제이다.
- 단, 판매 이후 하루는 주식 매매가 불가능하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sold는 매매한 이익을 담는 변수로 0으로, 초기화한다.
- hold는 매매하지 않았을 경우 차익을 저장할 변수로, Integer의 최소값으로 초기화한다.
- rest는 아무것도 하지 않았을 경우 이익을 저장하기 위한 변수로, 0으로 초기화한다.

3. prices를 반복하여 최대 이익을 구한다.
- hold에 hold와 차익이 되는 $rest - price$의 값 중 큰 값을 넣어준다.
- rest에 rest와 sold의 값 중 큰 값을 넣어준다.
- sold에 매매 이익이 되는 $hold + price$ 값을 넣어준다.

4. 반복이 완료되면 마지막으로 매매를 한 경우인 sold와 매매하지 않았을 경우인 rest중 큰 값이 최대 이익이므로, 해당 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BestTimeToBuyAndSellStockWithCooldown.java){:target="_blank"}에서 확인 가능합니다.