---
title: "Leetcode Java Non-negative Integers without Consecutive Ones"
excerpt: "Leetcode Non-negative Integers without Consecutive Ones Java"
last_modified_at: 2022-07-29T21:00:00
header:
  image: /assets/images/leetcode/non-negative-integers-without-consecutive-ones.png
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
[Link](https://leetcode.com/problems/non-negative-integers-without-consecutive-ones/){:target="_blank"}

# 코드
```java
class Solution {

  public int findIntegers(int n) {
    int[] dp = new int[32];
    dp[0] = 1;
    dp[1] = 2;
    for (int i = 2; i < dp.length; i++) {
      dp[i] = dp[i - 1] + dp[i - 2];
    }
    int sum = 0;
    int pre = 0;
    for (int idx = 30; idx >= 0; idx--) {
      if ((n & (1 << idx)) != 0) {
        sum += dp[idx];
        if (pre == 1) {
          sum--;
          break;
        }
        pre = 1;
      } else {
        pre = 0;
      }
    }
    return sum + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/759813465/){:target="_blank"}

# 설명
1. 양의 정수 n이 주어지면 [0, n] 범위의 정수 중 이진수로 변환했을 때 1이 연속되지 않은 정수의 개수를 반환하는 문제이다.

2. dp를 정수 최대 길이인 32 크기로 초기화 하고, 1과 2를 차례대로 넣어준 후 피보나치 수열을 이용하여 dp를 초기화한다.

3. 정수의 개수를 넣을 sum와 이전 자리의 이진수의 값을 저장할 pre를 0으로 초기화한다.

4. 30부터 0 이상까지 idx를 감소시키며 아래를 반복한다.
- n과 1을 idx번 이동시킨 값의 결과가 0이 아닌 경우, 아래를 수행한다.
  - sum에 dp의 idx번째 값을 더해 문제의 조건을 만족하는 정수의 개수를 증가시켜준다.
  - pre가 1인 경우, 연속된 1이 발생했으므로 sum을 감소시키고 반복을 중지한다.
- 위의 경우가 아닌 경우, pre에 0을 넣고 반복을 계속 수행한다.

5. 반복이 완료되면 [1, n] 범위의 정수 중 이진수로 변환했을 때 1이 연속되지 않은 정수의 개수인 sum에 0인 경우를 추가한 $sum + 1$을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NonNegativeIntegersWithoutConsecutiveOnes.java){:target="_blank"}에서 확인 가능합니다.