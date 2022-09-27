---
title: "Leetcode Java Longest Continuous Increasing Subsequence"
excerpt: "Leetcode Longest Continuous Increasing Subsequence Java"
last_modified_at: 2022-09-27T19:10:00
header:
  image: /assets/images/leetcode/longest-continuous-increasing-subsequence.png
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
[Link](https://leetcode.com/problems/longest-continuous-increasing-subsequence){:target="_blank"}

# 코드
```java
class Solution {

  public int findLengthOfLCIS(int[] nums) {
    int result = 0;
    int count = 1;
    for (int idx = 1; idx < nums.length; idx++) {
      if (nums[idx - 1] < nums[idx]) {
        count++;
      } else {
        result = Math.max(result, count);
        count = 1;
      }
    }
    return Math.max(result, count);
  }


}
```

# 결과
[Link](https://leetcode.com/submissions/detail/809708790/){:target="_blank"}

# 설명
1. nums를 이용하여 점층적으로 증가하는 가장 긴 부분 배열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 점층적으로 증가하는 가장 긴 부분 배열의 길이를 저장할 변수로, 0으로 초기화한다.
- count는 점층적으로 증가하는 숫자의 수를 계산할 변수로, 첫 값을 포함하여 1로 초기화한다.

3. 1부터 nums의 길이 미만까지 idx를 증가시키며 아래를 수행한다.
- nums의 $idx - 1$번째 값이 idx번째 값보다 작은 경우 값이 증가하므로, count를 증가시킨다.
- 위의 경우가 아닌 경우 그 전까지가 증가하는 부분 배열이므로, result에 result와 count 중 큰 값을 넣어주고 count를 1로 초기화한다.

4. 반복이 완료되면 result와 마지막으로 계산된 부분 배열의 길이인 count중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestContinuousIncreasingSubsequence.java){:target="_blank"}에서 확인 가능합니다.