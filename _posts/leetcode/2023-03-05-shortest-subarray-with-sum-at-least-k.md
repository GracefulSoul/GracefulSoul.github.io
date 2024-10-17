---
title: "Leetcode Java Shortest Subarray with Sum at Least K"
excerpt: "Leetcode - 'Shortest Subarray with Sum at Least K' 문제 Java 풀이"
last_modified_at: 2023-03-05T18:30:00
header:
  image: /assets/images/leetcode/shortest-subarray-with-sum-at-least-k.png
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
[Link](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k){:target="_blank"}

# 코드
```java
class Solution {

  public int shortestSubarray(int[] nums, int k) {
    int length = nums.length;
    long[] sum = new long[length + 1];
    for (int i = 0; i < length; i++) {
      sum[i + 1] = sum[i] + nums[i];
    }
    int left = 0;
    int right = -1;
    int[] dp = new int[length + 1];
    int result = length + 1;
    for (int i = 0; i <= length; i++) {
      while (right - left + 1 > 0 && sum[i] - sum[dp[left]] >= k) {
        result = Math.min(result, i - dp[left]);
        left++;
      }
      while (right - left + 1 > 0 && sum[dp[right]] >= sum[i]) {
        right--;
      }
      dp[++right] = i;
    }
    return result == length + 1 ? -1 : result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/submissions/909458477/){:target="_blank"}

# 설명
1. nums 내 연속된 숫자의 합이 k인 부분 배열이 존재하는지 검증하여 해당 길이를 반환하는 문제이다.
- 단, 부분 배열이 존재하지 않으면 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- sum은 nums의 점층적인 값의 합을 저장할 배열로, length 크기보다 하나 더 큰 크기의 배열로 초기화한다.
- left와 right는 부분 배열의 구간을 찾기 위한 위치 변수로, 0과 -1로 초기화한다.
- dp는 부분 배열의 시작 위치를 위치 별 저장하기 위한 배열로, length 크기보다 하나 더 큰 크기의 배열로 초기화한다.
- result는 부분 배열의 길이를 저장할 변수로, 나올 수 없는 길이인 length보다 하나 더 큰 크기의 값으로 초기화한다.

3. 0부터 length 이하까지 i를 증가시키며 아래를 수행한다.
- $right - left + 1$의 값이 0보다 크고, sum의 i번째 값과 dp[left]번째 값의 차이가 k 이상인 경우, result에 result와 $i - dp[left]$ 중 작은 길이를 저장하고 left를 증가시킨다.
- $right - left + 1$의 값이 0보다 크고, sum의 dp[right]번째 값이 i번째 값보다 크거나 같은 경우, right를 감소시키며 부분 배열의 범위를 축소시킨다.
- right를 증가시키고 dp의 right번째 위치에 i를 넣어준다.

4. 반복이 완료되면 result가 초기 값인 $length + 1$인지 검증하여 동일하면 -1을, 아니면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestSubarrayWithSumAtLeastK.java){:target="_blank"}에서 확인 가능합니다.