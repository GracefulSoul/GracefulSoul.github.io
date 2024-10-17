---
title: "Leetcode Java House Robber"
excerpt: "Leetcode - 'House Robber' 문제 Java 풀이"
last_modified_at: 2021-10-02T11:00:00
header:
  image: /assets/images/leetcode/house-robber.png
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
[Link](https://leetcode.com/problems/house-robber/){:target="_blank"}

# 코드
```java
public class Solution {

  public int rob(int[] nums) {
    int length = nums.length;
    int[][] dp = new int[length + 1][2];
    for (int i = 0; i < length; i++) {
      dp[i + 1][0] = Math.max(dp[i][0], dp[i][1]);
      dp[i + 1][1] = nums[i] + dp[i][0];
    }
    return Math.max(dp[length][0], dp[length][1]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/564261227/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums를 이용하여 인접하지 않은 값들의 합이 가장 큰 값을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 주어진 배열 nums의 길이를 넣은 변수이다.
- dp는 문제 풀이에 필요한 DP를 만들기 위한 배열로, [$length + 1$][2] 사이즈로 초기화 한다.

3. nums를 순회하면서 주어진 dp를 초기화 한다.
- dp[$i + 1$][0]에는 이전 값들인 dp[i][0]의 값과 dp[i][1]의 값 중 큰 값을 넣어준다.
- dp[$i + 1$][1]에는 nums[i]와 dp[i][0]의 합을 넣어준다.
  - dp[i][0]의 값은 dp[$i - 1$][0]의 값과 dp[$i - 1$][1]의 값 중 큰 값이므로, nums[i]와 인접하지 않은 값이다.

4. 반복이 완료되면 각 인접하지 않은 값들의 합을 저장한 dp[length][0]의 값과 dp[length][1]의 값 중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HouseRobber.java){:target="_blank"}에서 확인 가능합니다.