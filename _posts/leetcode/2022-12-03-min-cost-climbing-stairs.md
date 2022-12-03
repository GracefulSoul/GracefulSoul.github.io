---
title: "Leetcode Java Min Cost Climbing Stairs"
excerpt: "Leetcode Min Cost Climbing Stairs Java"
last_modified_at: 2022-12-03T10:30:00
header:
  image: /assets/images/leetcode/min-cost-climbing-stairs.png
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
[Link](https://leetcode.com/problems/min-cost-climbing-stairs){:target="_blank"}

# 코드
```java
class Solution {

  public int minCostClimbingStairs(int[] cost) {
    int length = cost.length;
    int[] dp = new int[length];
    dp[0] = cost[0];
    dp[1] = cost[1];
    for (int idx = 2; idx < length; idx++) {
      dp[idx] = Math.min(dp[idx - 1], dp[idx - 2]) + cost[idx];
    }
    return Math.min(dp[length - 1], dp[length - 2]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/853663482/){:target="_blank"}

# 설명
1. 아래의 규칙을 이용하여 바닥부터 계단을 오르는 비용을 저장한 cost를 이용하여 계단 아래에서 맨 위까지 올라가기 위한 최소 비용을 찾는 문제이다.
- 계단은 비용 지불 후 한 번에 하나 혹은 두 계단을 오를 수 있다.
- 계단 시작 위치는 계단 아래인 인덱스가 0인 위치이거나, 한 계단 위인 인덱스가 1인 위치에서 시작 할 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 cost의 길이를 저장한 변수이다.
- dp는 최소 비용을 계산하기 위한 배열로, length 길이의 정수 배열로 초기화하고 dp의 첫 번째와 두 번째 위치에 cost의 첫 번째와 두 번째 값을 넣어준다.

3. 2부터 length 미만까지 idx를 증가시키면서 아래를 반복한다.
- dp의 idx번째 위치에 dp의 $idx - 2$번째 값과 $idx - 1$번째 값 중 작은 값인 최소 비용에 cost의 idx번째 값을 더한 값을 넣어준다.

4. 반복이 완료되면 dp의 $length - 2$번째 값과 $length - 1$번째 값 중 작은 값인 최소 비용을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinCostClimbingStairs.java){:target="_blank"}에서 확인 가능합니다.