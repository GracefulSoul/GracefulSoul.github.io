---
title: "Leetcode Java Longest Increasing Subsequence"
excerpt: "Leetcode - 'Longest Increasing Subsequence' 문제 Java 풀이"
last_modified_at: 2021-12-13T13:00:00
header:
  image: /assets/images/leetcode/longest-increasing-subsequence.png
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
[Link](https://leetcode.com/problems/longest-increasing-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public int lengthOfLIS(int[] nums) {
    int[] dp = new int[nums.length + 1];
    dp[0] = Integer.MIN_VALUE;
    int length = 0;
    for (int idx = 0; idx < nums.length; idx++) {
      int position = length;
      while (dp[position] >= nums[idx]) {
        position--;
      }
      if (position == length) {
        length++;
      }
      dp[position + 1] = nums[idx];
    }
    return length;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/601087702/){:target="_blank"}

# 설명
1. 주어진 정수 배열인 nums를 이용하여 오름차순으로 부분 배열을 만들 때 가장 길게 만들 수 있는 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 오름차순으로 부분 배열을 만들 때 순차적인 값을 저장할 배열로, nums의 길이보다 1 크게 정의하고 처음 값을 정수의 가장 작은 값으로 넣어준다.
- length는 오름차순으로 부분 배열을 만들 때 최대 길이를 저장하는 변수로 0으로 초기화한다.

3. nums를 처음부터 끝까지 반복하여 최대 길이 length를 구한다.
- position에 length를 넣어주고 dp[position]의 값보다 nums[idx]가 큰 값일 때 까지 반복하여 position을 감소시킨다.
- position이 length와 동일한 경우 dp의 다음 값에 들어갈 값이므로, length를 증가시킨다.
- dp[$position + 1$]에 nums[idx] 값을 넣어주고 반복을 계속 수행한다.

4. 반복이 종료되면 nums를 이용하여 오름차순으로 부분 배열을 만들 때 가장 길게 만들 수 있는 length를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestIncreasingSubsequence.java){:target="_blank"}에서 확인 가능합니다.