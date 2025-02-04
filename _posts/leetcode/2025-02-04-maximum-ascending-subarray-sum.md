---
title: "Leetcode Java Maximum Ascending Subarray Sum"
excerpt: "Leetcode - 'Maximum Ascending Subarray Sum' 문제 Java 풀이"
last_modified_at: 2025-02-04T19:30:00
header:
  image: /assets/images/leetcode/maximum-ascending-subarray-sum.png
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
[Link](https://leetcode.com/problems/maximum-ascending-subarray-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxAscendingSum(int[] nums) {
    int result = nums[0];
    int curr = nums[0];
    for (int i = 1; i < nums.length; i++) {
      if (nums[i - 1] < nums[i]) {
        curr += nums[i];
      } else {
        curr = nums[i];
      }
      result = Math.max(result, curr);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-ascending-subarray-sum/submissions/1530899854/){:target="_blank"}

# 설명
1. nums의 연속된 값들 중 증가되는 부분 배열의 합이 최대인 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, nums의 첫 값을 저장한다.
- curr은 현재까지 부분 배열의 합을 저장할 변수로, result와 동일하게 nums의 첫 값을 저장한다.

3. 1부터 nums의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- nums[$i - 1$]의 값이 nums[i]의 값보다 작은 값이 증가하는 경우, curr에 nums[i]의 값을 더해준다.
- nums[$i - 1$]의 값이 nums[i]의 값보다 작지 않은 값이 증가하지 않는 경우, curr에 nums[i]의 값을 넣어준다.
- result에 result와 curr 중 가장 큰 값을 넣어준다.

4. 반복이 완료되면 증가되는 부분 배열의 합이 최대인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumAscendingSubarraySum.java){:target="_blank"}에서 확인 가능합니다.