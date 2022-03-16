---
title: "Leetcode Java Partition Equal Subset Sum"
excerpt: "Leetcode Partition Equal Subset Sum Java 풀이"
last_modified_at: 2022-03-16T12:00:00
header:
  image: /assets/images/leetcode/partition-equal-subset-sum.png
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
[Link](https://leetcode.com/problems/partition-equal-subset-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canPartition(int[] nums) {
    int sum = 0;
    for (int num : nums) {
      sum += num;
    }
    if ((sum & 1) > 0) {
      return false;
    }
    int target = sum / 2;
    return this.dfs(nums, new boolean[target + 1], 0, target);
  }

  private boolean dfs(int[] nums, boolean[] dp, int index, int target) {
    if (index >= nums.length) {
      return false;
    } else if (nums[index] == target) {
      return true;
    } else {
      int num = target - nums[index];
      if (num > 0 && !dp[num]) {
        dp[num] = true;
        return this.dfs(nums, dp, index + 1, num) || this.dfs(nums, dp, index + 1, target);
      } else {
        return this.dfs(nums, dp, index + 1, target);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/660906769/){:target="_blank"}

# 설명
1. 비어있지 않은 주어진 양의 정수 배열 nums를 이용하여 합이 동일한 두 부분 배열로 나눌 수 있는지 검증하는 문제이다.

2. sum에 nums의 모든 값을 더해 넣어준다.

3. sum과 1의 AND(&) 비트 연산 수행 결과가 0 이상인 sum이 홀수인 경우 두 값을 균일하게 나눌 수 없으므로, false를 반환한다.

4. target에 $\frac{sum}{2}$의 결과를 넣어주고, 5번에서 정의한 dfs(int[] nums, boolean[] dp, int index, int target) 함수를 dp에 $target + 1$ 크기의 부울 배열과 index는 0, target에 target을 이용하여 수행한 결과를 주어진 문제의 결과로 반환한다.

5. DFS 방식으로 결과를 탐색할 dfs(int[] nums, boolean[] dp, int index, int target) 메서드를 정의한다.
- index가 nums의 길이보다 크거나 같은 경우 균일한 두 값으로 나눌 수 없으므로, false를 반환한다.
- nums[index] 값이 target과 동일한 경우, true를 반환한다.
- 그 외의 경우 아래를 수행한다.
  - num에 target과 nums의 index번째 값의 차이를 넣어준다.
  - num이 0보다 크고 dp의 num번째 자리가 false인 경우, dp의 num번째 값을 true로 바꾸고 index를 1 증가시키고 target에 num을 넣은 재귀 호출 결과와 index를 1 증가시킨 재귀 호출 결과의 OR 조건 결과를 반환한다.
  - 위의 경우가 아니면, index를 1 증가시킨 재귀 호출 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PartitionEqualSubsetSum.java){:target="_blank"}에서 확인 가능합니다.