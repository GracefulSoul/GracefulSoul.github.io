---
title: "Leetcode Java Minimum Cost to Make Array Equal"
excerpt: "Leetcode Minimum Cost to Make Array Equal Java"
last_modified_at: 2023-06-21T19:00:00
header:
  image: /assets/images/leetcode/minimum-cost-to-make-array-equal.png
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
[Link](https://leetcode.com/problems/minimum-cost-to-make-array-equal){:target="_blank"}

# 코드
```java
class Solution {

  public long minCost(int[] nums, int[] cost) {
    int left = Integer.MAX_VALUE;
    int right = Integer.MIN_VALUE;
    for (int num : nums) {
      left = Math.min(num, left);
      right = Math.max(num, right);
    }
    long result = 0;
    while (left < right) {
      int mid = left + ((right - left) / 2);
      long cost1 = this.getCost(nums, cost, mid);
      long cost2 = this.getCost(nums, cost, mid + 1);
      result = Math.min(cost1, cost2);
      if (cost1 < cost2) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }
    return result;
  }

  private long getCost(int[] nums, int[] cost, long num) {
    long sum = 0L;
    for (int i = 0; i < nums.length; i++) {
      sum += Math.abs(nums[i] - num) * cost[i];
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-cost-to-make-array-equal/submissions/976249205/){:target="_blank"}

# 설명
1. nums[i]의 값을 1씩 증가시킬 때 드는 비용이 cost[i]일 때, nums의 모든 값을 동일한 값으로 맞출 경우 드는 최소 비용을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- left와 right는 nums의 최소 값인 좌측 탐색 위치와 최대 값인 우측 탐색 위치를 넣을 변수로, nums를 반복하여 최솟값과 최댓값을 넣어준다.
- result는 nums의 모든 값을 동일한 값으로 맞출 경우 드는 최소 비용을 저장할 변수로, 0으로 초기화한다.

3. left가 right 미만일 때까지 아래를 반복한다.
- mid에 $left + \frac{right - left}{2}$의 중앙값을 넣어준다.
- cost1에 4번에서 정의한 getCost(int[] nums, int[] cost, long index)를 index에 mid를 넣어 수행한 결과를 넣어준다.
- cost2에 4번에서 정의한 getCost(int[] nums, int[] cost, long index)를 index에 $mid + 1$을 넣어 수행한 결과를 넣어준다.
- cost1이 cost2보다 작은 경우, right에 mid를 넣어 범위를 좁혀준다.
- cost1이 cost2보다 작지 않은 경우, left에 $mid + 1$을 넣어 범위를 좁혀준다.

4. index를 기준으로 비용의 합을 계산할 getCost(int[] nums, int[] cost, long index) 메서드를 정의한다.
- sum은 비용의 합계를 넣을 변수로, nums의 값을 num을 뺀 변경 횟수에 cost의 비용을 곱한 값을 넣어 반환한다.

5. 반복이 완료되면 최소 비용이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumCostToMakeArrayEqual.java){:target="_blank"}에서 확인 가능합니다.