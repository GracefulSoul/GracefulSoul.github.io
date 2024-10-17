---
title: "Leetcode Java Number of Longest Increasing Subsequence"
excerpt: "Leetcode - 'Number of Longest Increasing Subsequence' 문제 Java 풀이"
last_modified_at: 2022-09-26T19:40:00
header:
  image: /assets/images/leetcode/number-of-longest-increasing-subsequence.png
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
[Link](https://leetcode.com/problems/number-of-longest-increasing-subsequence){:target="_blank"}

# 코드
```java
class Solution {

  public int findNumberOfLIS(int[] nums) {
    int length = nums.length;
    int result = 0;
    int max = 0;
    int[] dp = new int[length];
    int[] count = new int[length];
    for (int i = 0; i < length; i++) {
      dp[i] = count[i] = 1;
      for (int j = 0; j < i; j++) {
        if (nums[i] > nums[j]) {
          if (dp[i] == dp[j] + 1) {
            count[i] += count[j];
          } else if (dp[i] < dp[j] + 1) {
            dp[i] = dp[j] + 1;
            count[i] = count[j];
          }
        }
      }
      if (max == dp[i]) {
        result += count[i];
      } else if (max < dp[i]) {
        max = dp[i];
        result = count[i];
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/808950171/){:target="_blank"}

# 설명
1. nums를 이용하여 가장 긴 부분 배열의 수를 구하는 문제이다.
- 단, 위의 부분 배열은 연속된 요소가 점층적으로 증가하여야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 가장 긴 배열의 개수를 계산하기 위한 변수로, 0으로 초기화한다.
- max는 가장 긴 배열의 길이를 저장하기 위한 변수로, 0으로 초기화한다.
- dp는 nums의 각 위치 값으로 끝나는 가장 긴 부분 배열의 길이를 저장할 배열로, length 크기로 초기화한다.
- count는 nums의 각 위치 값으로 끝나는 가장 긴 부분 배열의 수를 저장할 배열로, length 크기로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
- dp와 count의 i번째 위치를 1로 초기화한다.
- 0부터 i 미만까지 j를 증가시키며, nums[i]가 nums[j]보다 크면 부분 배열에 포함 가능하므로 아래를 수행한다.
  - dp[i]의 값과 $dp[j] + 1$이 같은 경우 dp[j]에 해당하는 부분 배열들에 nums[i]만 마지막 값에 추가하면 전체 부분 배열에 포함되므로, count[i]의 값에 count[j]의 값을 더해준다.
  - dp[i]의 값이 $dp[j] + 1$보다 작은 경우 이전 값보다 긴 부분 배열이 발견되었으므로, dp[i]에 $dp[j] + 1$을 넣어주고 count[i]에 count[j]를 넣어준다.
- max와 dp[i]가 동일한 경우, result에 count[i]를 넣어 가장 긴 부분 배열의 수를 더해준다.
- max가 dp[i]보다 작은 경우, max에 dp[i]를 넣고 result에 count[i]를 넣어 최대 길이와 해당 길이의 부분 배열 수를 현재 값으로 초기화한다.

4. 반복이 완료되면 조건을 충족하는 가장 긴 부분 배열의 수를 계산한 result를 주어진 문제의 결과로 반환한다. 

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SecondMinimumNodeInABinaryTree.java){:target="_blank"}에서 확인 가능합니다.