---
title: "Leetcode Java Target Sum"
excerpt: "Leetcode Target Sum Java 풀이"
last_modified_at: 2022-05-15T09:00:00
header:
  image: /assets/images/leetcode/target-sum.png
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
[Link](https://leetcode.com/problems/target-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public int findTargetSumWays(int[] nums, int target) {
    int sum = 0;
    for (int num : nums) {
      sum += num;
    }
    return sum < target || (sum + target) % 2 == 1 ? 0 : this.subset(nums, (target + sum) >> 1);
  }

  private int subset(int[] nums, int target) {
    if (target < 0) {
      return 0;
    }
    int[] dp = new int[target + 1];
    dp[0] = 1;
    for (int num : nums) {
      for (int idx = target; idx >= num; idx--) {
        dp[idx] += dp[idx - num];
      }
    }
    return dp[target];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/699619428/){:target="_blank"}

# 설명
1. nums의 각 숫자 사이에 '+'와 '-'를 넣어 해당 수식의 결과가 target이 되는 경우의 수를 구하는 문제이다.

2. sum은 nums의 모든 숫자들의 합을 저장할 변수로, nums를 반복하여 모든 값을 더해준다.

3. target이 sum보다 크거나 sum과 target을 합한 결과가 홀수인지를 이용하여 아래의 각 경우 별 수행을 한다.
- 위의 결과들 중 하나라도 만족하는 경우 수식을 만들 수 없으므로, 0을 주어진 문제의 결과로 반환한다.
- 위의 결과들 중 하나라도 만족하지 않는 경우, 4번에서 정의한 subset(int[] nums, int target) 메서드를 수행한 값을 주어진 문제의 결과로 반환한다.

4. dp를 활용한 subset으로 경우의 수를 구하기 위한 subset(int[] nums, int target) 메서드를 정의한다.
- target이 0보다 작은 경우 수식을 만들 수 있는 경우의 수가 없으므로, 0을 반환한다.
- dp는 경우의 수를 구하기 위해 사용될 배열로, $target + 1$ 크기로 정의하고 첫 값을 1로 초기화한다.
- nums의 모든 값을 반복하고, target 부터 num 보다 클 때 까지 idx를 감소시키며 반복하여 아래를 수행한다.
  - dp의 idx번째 위치의 값에 dp의 $idx - num$의 결과를 더해 경우의 수를 계산한다.
  - idx를 감소시키며 dp의 $idx - num$의 결과를 더하는 이유는, 해당 결과는 현재의 num을 아직 고려하지 않은 부분 집합의 결과이기 때문에 동일한 num을 반복 사용하지 않는다.
- 반복이 완료되면 경우의 수인 dp의 target번째 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TargetSum.java){:target="_blank"}에서 확인 가능합니다.