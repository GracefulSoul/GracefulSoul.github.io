---
title: "Leetcode Java Number of Ways to Stay in the Same Place After Some Steps"
excerpt: "Leetcode Number of Ways to Stay in the Same Place After Some Steps Java"
last_modified_at: 2023-10-15T16:20:00
header:
  image: /assets/images/leetcode/number-of-ways-to-stay-in-the-same-place-after-some-steps.png
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
[Link](https://leetcode.com/problems/number-of-ways-to-stay-in-the-same-place-after-some-steps){:target="_blank"}

# 코드
```java
class Solution {

  public int numWays(int steps, int arrLen) {
    int length = Math.min(steps, arrLen);
    long[][] dp = new long[steps + 1][length + 1];
    dp[0][0] = 1;
    for (int i = 0; i < steps; i++) {
      for (int j = 0; j < length; j++) {
        dp[i + 1][j] = (dp[i][j] + dp[i][j + 1] + (j > 0 ? dp[i][j - 1] : 0)) % 1000000007;
      }
    }
    return (int) dp[steps][0];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-ways-to-stay-in-the-same-place-after-some-steps/submissions/1075667008/){:target="_blank"}

# 설명
1. arrLen 크기의 배열의 첫 위치에서 steps번 이동 혹은 이동하지 않는 선택을 통해 첫 위치로 끝날 수 있는 경우의 수를 구하는 문제이다.
- 단, 방법의 수가 매우 클 수 있으므로 모듈러 $10^9 + 7$를 사용하여 값을 계산한다.

2. 문제 풀이에 필요한 변수를 저의한다.
- length는 최대 이동 가능 거리를 저장할 변수로, steps와 arrLen 중 작은 값을 넣어준다.
- dp는 경우의 수를 계산하기 위한 배열로, $(steps + 1) \times (length + 1)$ 크기의 2차원 정수 배열로 초기화하고 첫 값에 1을 넣어준다.

3. 0부터 steps 미만까지 i를 증가시키고, 0부터 length 미만까지 j를 증가시키며 아래를 수행한다.
- dp[$i + 1$][j] 위치에 아래의 값들을 더한 후 $10^9 + 7$로 나눈 값을 넣어준다.
  - 이전 위치까지 이동 횟수인 dp[i][j]의 값
  - 이전 위치에서 이동 범위를 늘린 dp[i][$j + 1$]의 값
  - j가 0보다 큰 이동 범위가 존재하는 경우, 이전 위치까지의 경우의 수인 dp[i][$j - 1$]의 값 혹은 첫 수행인 경우 0.

4. 반복이 완료되면 경우의 수가 저장된 dp[steps][0]의 값을 주어진 문제의 결과로 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfWaysToStayInTheSamePlaceAfterSomeSteps.java){:target="_blank"}에서 확인 가능합니다.