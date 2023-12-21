---
title: "Leetcode Java Buy Two Chocolates"
excerpt: "Leetcode Buy Two Chocolates Java"
last_modified_at: 2023-12-21T19:40:00
header:
  image: /assets/images/leetcode/buy-two-chocolates.png
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
[Link](https://leetcode.com/problems/buy-two-chocolates){:target="_blank"}

# 코드
```java
class Solution {

  public int buyChoco(int[] prices, int money) {
    int[] mins = new int[] { Integer.MAX_VALUE, Integer.MAX_VALUE };
    for (int price : prices) {
      if (price < mins[0]) {
        mins[1] = mins[0];
        mins[0] = price;
      } else {
        mins[1] = Math.min(mins[1], price);
      }
    }
    int leftover = money - (mins[0] + mins[1]);
    return leftover >= 0 ? leftover : money;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/buy-two-chocolates/submissions/1125003496/){:target="_blank"}

# 설명
1. prices의 가격을 가진 초콜릿들 중 가장 낮은 가격의 초콜릿 두 개를 money 내 구입한 후 남은 가격을 반환하는 문제이다.
- 만일 money로 가장 낮은 가격의 초콜릿 두 개를 사지 못한다면 money를 주어진 문제의 결과로 반환한다.

2. mins는 가장 작은 가격의 초콜릿 가격을 담기 위한 변수로, 2 크기의 정수 배열로 정의하여 각 값을 정수의 최댓값으로 초기화하여 prices의 모든 값을 순차적으로 반복하여 mins에 가장 낮은 가격의 초콜릿 두 개의 가격을 넣어준다.

3. leftover는 money에서 두 초콜릿의 가격을 뺀 잔돈으로, 주어진 문제의 결과로 0 이상이면 leftover를 아니면 money를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/leftover .java){:target="_blank"}에서 확인 가능합니다.