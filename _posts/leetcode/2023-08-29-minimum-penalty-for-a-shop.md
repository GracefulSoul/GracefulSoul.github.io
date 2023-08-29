---
title: "Leetcode Java Minimum Penalty for a Shop"
excerpt: "Leetcode Minimum Penalty for a Shop Java"
last_modified_at: 2023-08-29T18:40:00
header:
  image: /assets/images/leetcode/minimum-penalty-for-a-shop.png
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
[Link](https://leetcode.com/problems/minimum-penalty-for-a-shop){:target="_blank"}

# 코드
```java
class Solution {

  public int bestClosingTime(String customers) {
    int max = 0;
    int score = 0;
    int time = -1;
    for (int i = 0; i < customers.length(); i++) {
      if (customers.charAt(i) == 'Y') {
        score++;
      } else {
        score--;
      }
      if (score > max) {
        max = score;
        time = i;
      }
    }
    return time + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-penalty-for-a-shop/submissions/1034898957/){:target="_blank"}

# 설명
1. 'Y'와 'N'로 이루어진 고객 방문 기록인 customers를 이용하여 최소 벌금을 부과하기 위해 가장 빨리 폐점하는 시간을 반환하는 문제이다.
- i번째 문자가 'Y'인 경우, 고객이 i번째 시간에 도착한다는 의미이다.
- i번째 문자가 'N'인 경우, 고객이 i번째 시간에 오지 않는다는 의미를 나타낸다.
- 0 <= j <= n인 j 시간에 상점이 닫을 때 까지 아래와 같이 벌금이 부과된다.
  - 매장이 문을 열고 손님이 오는 경우.
  - 매장이 문을 닫고 손님이 오는 경우.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 최대 값을 저장할 변수로, 0으로 초기화한다.
- score는 벌금을 저장할 변수로, 0으로 초기화한다.
- time은 가장 빨리 폐점하는 시간을 저장할 변수로, -1로 초기화한다.

3. 0부터 customers의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- customers의 i번째 값이 'Y'인 경우, 벌금을 부과하지 않았으므로 score를 증가시키고 아니면 score를 감소시켜 벌금을 부과한다.
- score가 max보다 큰 경우, max에 최대 값을 저장하고 time에 현재까지 영업한 시간인 i를 넣어준다.

4. 반복이 완료되면 최소 벌금을 부과하는 시간인 $time + 1$을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumPenaltyForAShop.java){:target="_blank"}에서 확인 가능합니다.