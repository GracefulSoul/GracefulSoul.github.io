---
title: "Leetcode Java Time Needed to Buy Tickets"
excerpt: "Leetcode Time Needed to Buy Tickets Java"
last_modified_at: 2024-04-09T18:00:00
header:
  image: /assets/images/leetcode/time-needed-to-buy-tickets.png
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
[Link](https://leetcode.com/problems/time-needed-to-buy-tickets/){:target="_blank"}

# 코드
```java
class Solution {

  public int timeRequiredToBuy(int[] tickets, int k) {
    int result = 0;
    for (int i = 0; i < tickets.length; i++) {
      if (i <= k) {
        result += Math.min(tickets[i], tickets[k]);
      } else {
        result += Math.min(tickets[i], tickets[k] - 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/time-needed-to-buy-tickets/submissions/1227468702/){:target="_blank"}

# 설명
1. 사람 별 티켓 구매 수량이 저장된 tickets를 이용하여 아래의 규칙을 만족하면서 k번째 사람이 티켓 구매가 완료하는데까지 필요한 시간을 계산하는 문제이다.
- tickets의 0번째 대기 순서는 맨 앞, 마지막 대기 순서는 맨 마지막이다.
- 한 사람이 티켓을 구매하는데 1초가 걸리며, 한 사람에 한 장만 구매가 가능하다.
- 구매한 사람은 다음 티켓을 구매하기 위해서 맨 뒤로 이동해야 한다.
- 구매하려던 수량의 티켓을 모두 구매한 사람은 대기열에서 나온다.

2. result는 k번째 사람이 티켓 구매를 완료하는데까지 필요한 시간을 저장하기 위한 변수로, 0으로 초기화한다.

3. 0부터 tickets의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- i가 k 이하인 경우, result에 tickets[i]와 tickets[k] 중 작은 값을 더해 구매 수량에 필요한 시간을 계산해준다.
- 위의 경우가 아니라면, result에 tickets[i]와 $tickets[k] - 1$ 중 작은 값을 더해 k번째 사람이 구매 후 티켓과 비교하여 시간을 계산해준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TimeNeededToBuyTickets.java){:target="_blank"}에서 확인 가능합니다.