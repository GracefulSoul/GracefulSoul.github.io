---
title: "Leetcode Java Minimum Cost For Tickets"
excerpt: "Leetcode Minimum Cost For Tickets Java"
last_modified_at: 2023-08-28T20:40:00
header:
  image: /assets/images/leetcode/minimum-cost-for-tickets.png
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
[Link](https://leetcode.com/problems/minimum-cost-for-tickets){:target="_blank"}

# 코드
```java
class Solution {

  public int mincostTickets(int[] days, int[] costs) {
    int last = days[days.length - 1];
    boolean[] planned = new boolean[last + 1];
    for (int day : days) {
      planned[day] = true;
    }
    int[] dp = new int[last + 1];
    for (int i = 1; i <= last; i++) {
      if (!planned[i]) {
        dp[i] = dp[i - 1];
        continue;
      }
      dp[i] = dp[i - 1] + costs[0];
      dp[i] = Math.min(dp[i], dp[Math.max(i - 7, 0)] + costs[1]);
      dp[i] = Math.min(dp[i], dp[Math.max(i - 30, 0)] + costs[2]);
    }
    return dp[last];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-cost-for-tickets/submissions/1034004373/){:target="_blank"}

# 설명
1. days에 해당하는 날자만큼 여행을 하려고 할 때, 각 패스권의 가격이 담긴 costs를 활용하여 최소 여행 경비를 반환하는 문제이다.
- 패스권은 1, 7, 30일권으로 해당 가격은 순차적으로 costs에 들어있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- last는 여행의 마지막 날을 저장할 변수로, days의 마지막 값을 넣어준다.
- planned는 여행 계획을 세운 날을 저장할 변수로, 여행 날자에 해당하는 위치의 값을 true로 저장해준다.
- dp는 최소 여행 경비를 계산하기 위한 변수로, $last + 1$ 크기의 정수 배열로 초기화한다.

3. 1부터 last 이하까지 i를 증가시키며 아래를 반복한다.
- planned[i]의 값이 false인 여행 일정이 아닌 경우, dp[i]에 $i - 1$번째 값을 넣고 다음 반복을 수행한다.
- dp[i]에 아래의 값들 중 가장 작은 값을 넣어준다.
  - 어제까지 경비와 1일 패스권 가격을 더한 값.
  - 7일 전 경비 혹은 처음부터 7일 패스권 가격을 더한 값.
  - 30일 전 경비 혹은 처음부터 30일 패스권 가격을 더한 값.

4. 반복이 완료되면 dp의 last번째 값인 최소 경비를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumCostForTickets.java){:target="_blank"}에서 확인 가능합니다.