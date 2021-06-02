---
title: "Leetcode Java Maximum Subarray"
excerpt: "Leetcode Maximum Subarray Java 풀이"
last_modified_at: 2021-06-02T17:00:00
header:
  image: /assets/images/leetcode/maximum-subarray.png
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
[Link](https://leetcode.com/problems/maximum-subarray/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSubArray(int[] nums) {
    int subSum = nums[0];
    int result = subSum;
    for (int idx = 1; idx < nums.length; idx++) {
      subSum = Math.max(subSum + nums[idx], nums[idx]);
      result = Math.max(result, subSum);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/501772060/){:target="_blank"}

# 설명
1. 주어진 배열 nums의 부분 합이 가장 큰 값을 구하는 문제이다.

2. 부분 합을 저장하는 subSum은 초기 값을 주어진 배열 nums의 첫 값을 주입하고, 가장 큰 부분 합의 값을 저장하는 result 또한 같은 값으로 정의한다.

3. 주어진 배열 nums를 두 번째 값부터 부분 합을 구하여 최대가 되는 값을 구한다.
- 초기화를 주어진 배열 nums의 첫 값으로 하였으므로, 두 번째 값부터 반복문을 수행한다.
- subSum을 주어진 배열 nums의 값을 더한 값과, subSum 값 중 큰 값을 subSum에 저장한다.
- result와 subSum의 값 중 가장 큰 값을 result 변수에 저장한다.

4. 반복이 종료되면, 가장 큰 부분 합을 저장한 변수 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumSubarray.java){:target="_blank"}에서 확인 가능합니다.