---
title: "Leetcode Java Combination Sum IV"
excerpt: "Leetcode Combination Sum IV Java 풀이"
last_modified_at: 2022-02-06T11:00:00
header:
  image: /assets/images/leetcode/combination-sum-iv.png
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
[Link](https://leetcode.com/problems/combination-sum-iv/){:target="_blank"}

# 코드
```java
class Solution {

  public int combinationSum4(int[] nums, int target) {
    int[] dp = new int[target + 1];
    Arrays.fill(dp, -1);
    return this.resursive(nums, dp, target);
  }

  private int resursive(int[] nums, int[] dp, int target) {
    if (target == 0) {
      return 1;
    } else if (target < 0) {
      return 0;
    } else if (dp[target] == -1) {
      int result = 0;
      for (int num : nums) {
        result += this.resursive(nums, dp, target - num);
      }
      dp[target] = result;
    }
    return dp[target];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/635345142/){:target="_blank"}

# 설명
1. 주어진 정수 배열인 nums가 주어지면 같은 위치의 값을 반복 사용하더라도 목표 target을 만들기 위한 고유 조합의 개수를 구하는 문제이다.

2. 문제 풀이에 필요한 dp를 $target + 1$ 크기로 정의하고, 모든 값을 -1로 초기화한다.

3. 4번에서 정의한 재귀 호출 메서드인 resursive(int[] nums, int[] dp, int target)를 호출한 결과를 주어진 문제의 결과로 반환한다.

4. 재귀 호출을 통해 목표된 값을 탐색하기 위한 resursive(int[] nums, int[] dp, int target) 메서드를 정의한다.
- target이 0인 경우 목표 값을 완성한 경우이므로, 1을 반환한다.
- target이 0보다 작은 경우 목표값을 초과한 경우이므로, 0을 반환한다.
- dp의 target번째 값이 -1인 경우 해당 위치의 dp가 초기화되지 않았다는 의미이므로, 아래를 수행하여 값을 넣어준다.
  - result에 0을 넣어준다.
  - nums를 순회하여 result에 target에 num을 감소시키며 재귀 호출을 수행하여 개수를 넣어준다.
  - dp의 target번째 위치에 result를 넣어준다.
- dp의 target번째 값을 반환하여 해당 target번째 값의 고유 조합의 개수를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CombinationSumIV.java){:target="_blank"}에서 확인 가능합니다.