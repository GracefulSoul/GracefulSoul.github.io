---
title: "Leetcode Java Longest Strictly Increasing or Strictly Decreasing Subarray"
excerpt: "Leetcode - 'Longest Strictly Increasing or Strictly Decreasing Subarray' 문제 Java 풀이"
last_modified_at: 2025-02-03T18:30:00
header:
  image: /assets/images/leetcode/longest-strictly-increasing-or-strictly-decreasing-subarray.png
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
[Link](https://leetcode.com/problems/longest-strictly-increasing-or-strictly-decreasing-subarray/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestMonotonicSubarray(int[] nums) {
    int result = 1;
    int increase = 1;
    int decrease = 1;
    for (int i = 1; i < nums.length; i++) {
      if (nums[i - 1] < nums[i]) {
        increase++;
        decrease = 1;
      } else if (nums[i - 1] > nums[i]) {
        decrease++;
        increase = 1;
      } else {
        increase = 1;
        decrease = 1;
      }
      result = Math.max(result, Math.max(increase, decrease));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/submissions/1529596251/){:target="_blank"}

# 설명
1. nums의 연속된 값들을 이용하여 증가하는 값의 길이와 감소하는 값의 길이 중 가장 긴 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 가장 긴 길이를 저장하기 위한 변수로, 첫 값을 포함한 최소 길이인 1로 초기화한다.
- increase와 decrease는 증가하거나 감소하는 연속된 값의 갯수를 계산하기 위한 변수로, result와 동일한 이유로 둘 다 1로 초기화한다.

3. 1부터 nums의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- nums[i - 1]의 값이 nums[i]의 값보다 작으면 값이 증가하고 있으므로, increase를 증가시키고 decrease를 1로 초기화한다.
- nums[i - 1]의 값이 nums[i]의 값보다 크면 값이 감소하고 있으므로, decrease를 증가시키고 increase를 1로 초기화한다.
- 그 외의 경우 값이 동일하므로, increase와 decrease를 1로 초기화한다.
- result에 result, increase, decrease 중 큰 값을 넣어 현재까지 가장 긴 길이를 저장한다.

4. 반복이 완료되어 구해진 가장 긴 길이인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestStrictlyIncreasingOrStrictlyDecreasingSubarray.java){:target="_blank"}에서 확인 가능합니다.