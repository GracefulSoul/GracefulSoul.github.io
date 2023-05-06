---
title: "Leetcode Java Maximum Sum Circular Subarray"
excerpt: "Leetcode Maximum Sum Circular Subarray Java"
last_modified_at: 2023-05-07T07:20:00
header:
  image: /assets/images/leetcode/maximum-sum-circular-subarray.png
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
[Link](https://leetcode.com/problems/maximum-sum-circular-subarray){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSubarraySumCircular(int[] nums) {
    int max1 = this.getMaximumSubarray(nums);
    int sum = 0;
    for (int i = 0; i < nums.length; i++) {
      sum += nums[i];
      nums[i] = -nums[i];
    }
    int max2 = sum + this.getMaximumSubarray(nums);
    if (max2 == 0) {
      return max1;
    } else {
      return Math.max(max1, max2);
    }
  }

  private int getMaximumSubarray(int[] nums) {
    int sum = nums[0];
    int max = nums[0];
    for (int i = 1; i < nums.length; i++) {
      sum = Math.max(sum + nums[i], nums[i]);
      max = Math.max(max, sum);
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-sum-circular-subarray/submissions/945710118/){:target="_blank"}

# 설명
1. 원형으로 이어진 숫자들이 저장된 nums를 이용하여 비어있지 않은 부분 배열의 최대 합을 반환하는 문제이다.

2. max1에 nums를 이용하여 원형이 아닌 상태에서 부분 배열의 최대 합을 3번에서 정의한 getMaximumSubarray(int[] nums) 메서드 수행한 결과를 넣어준다.

3. [Kadane's Algorithm](https://en.wikipedia.org/wiki/Maximum_subarray_problem#Kadane's_algorithm){:target="_blank"}을 이용하여 부분 배열의 최대 합을 구하기 위한 getMaximumSubarray(int[] nums)를 정의한다.
- 부분 배열의 최대 합을 구하기 위한 변수를 정의한다.
  - sum은 부분 배열의 최대 합을 계산하기 위한 변수로, nums의 첫 번째 값으로 초기화한다.
  - max는 부분 배열의 최대 합이 가장 큰 값을 구하기 위한 변수로, nums의 첫 번째 값을 초기화한다.
- 1부터 nums의 길이 미만까지 i를 증가시키며 아래를 수행한다.
  - sum에 sum에 nums의 i번째 값을 더한 값과 nums의 i번째 값 중 큰 값을 넣어준다.
  - max에는 max와 sum 중 큰 부분 배열의 합을 넣어준다.
- 구해진 부분 배열의 최대 합이 저장된 max를 반환한다.

4. sum을 0으로 초기화하고 nums의 모든 값을 이용하여 합을 넣고, 모든 값을 음수/양수로 반전시킨다.

5. max2에 nums를 이용하여 원현인 상태에서 부분 배열의 최대 합을 3번에서 정의한 getMaximumSubarray(int[] nums) 메서드 수행한 결과에 sum을 더해서 넣어준다.

6. max2가 0인 경우, max1을 아니면 max1과 max2 중 큰 값을 주어진 문제의 결과로 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumSumCircularSubarray.java){:target="_blank"}에서 확인 가능합니다.