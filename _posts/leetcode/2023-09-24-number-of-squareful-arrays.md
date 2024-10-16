---
title: "Leetcode Java Number of Squareful Arrays"
excerpt: "Leetcode Number of Squareful Arrays Java"
last_modified_at: 2023-09-24T12:00:00
header:
  image: /assets/images/leetcode/number-of-squareful-arrays.png
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
[Link](https://leetcode.com/problems/number-of-squareful-arrays){:target="_blank"}

# 코드
```java
class Solution {

  public int numSquarefulPerms(int[] nums) {
    return this.dfs(nums, 0);
  }

  private int dfs(int[] nums, int index) {
    if (index >= nums.length) {
      return 1;
    }
    int sum = 0;
    for (int i = index; i < nums.length; i++) {
      if (!this.isSwapable(nums, index, i)) {
        continue;
      }
      this.swap(nums, index, i);
      if (index == 0 || this.isSquareful(nums, index)) {
        sum += this.dfs(nums, index + 1);
      }
      this.swap(nums, index, i);
    }
    return sum;
  }

  private boolean isSwapable(int[] nums, int i, int j) {
    while (i < j) {
      if (nums[i++] == nums[j]) {
        return false;
      }
    }
    return true;
  }

  private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
  }

  private boolean isSquareful(int[] nums, int idx) {
    int sqrt = (int) Math.sqrt(nums[idx] + nums[idx - 1]);
    return (sqrt * sqrt) == (nums[idx] + nums[idx - 1]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-squareful-arrays/submissions/1057548265/){:target="_blank"}

# 설명
1. nums의 좌우 값의 합이 완전 제곱이 되도록 정렬 가능한 경우의 수를 반환하는 문제이다.
- 완전 제곱은 한 정수에 대한 제곱 값에 해당하는 경우를 의미한다.

2. 3번에서 정의한 dfs(int[] nums, int index) 메서드의 index에 0을 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 검증할 dfs(int[] nums, int index) 메서드를 정의한다.
- index가 nums의 길이 이상인 경우, 다음 검증이 불가능하므로 1을 반환한다.
- sum은 경우의 수를 더할 변수로, 0으로 초기화한다.
- index부터 nums의 길이 미만까지 i를 증가시켜 아래를 반복한다.
  - 동일한 수가 이어져 스왑이 필요 없는 경우, 다음 반복을 수행한다.
  - nums의 index번째 값과 i번째 값을 스왑해준다.
  - index가 0이거나 완전 제곱을 만족하는 경우, sum에 $index + 1$로 재귀 호출을 수행한 결과를 더해준다.
  - 위의 수행이 완료되면 nums의 index번째 값과 i번째 값을 스왑하여 원복해준다.
- 반복이 완료되면 sum을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestStringChain.java){:target="_blank"}에서 확인 가능합니다.