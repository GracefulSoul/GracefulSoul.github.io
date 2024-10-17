---
title: "Leetcode Java Max Dot Product of Two Subsequences"
excerpt: "Leetcode Hard - 'Max Dot Product of Two Subsequences' 문제 Java 풀이"
last_modified_at: 2023-10-06T22:00:00
header:
  image: /assets/images/leetcode/max-dot-product-of-two-subsequences.png
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
[Link](https://leetcode.com/problems/max-dot-product-of-two-subsequences){:target="_blank"}

# 코드
```java
class Solution {

  public int maxDotProduct(int[] nums1, int[] nums2) {
    int nums1Length = nums1.length;
    int nums2Length = nums2.length;
    int[][] dp = new int[nums1Length + 1][nums2Length + 1];
    for (int[] r : dp) {
      Arrays.fill(r, Integer.MIN_VALUE);
    }
    for (int i = 0; i < nums1Length; i++) {
      for (int j = 0; j < nums2Length; j++) {
        dp[i + 1][j + 1] = Math.max(Math.max(dp[i][j + 1], dp[i + 1][j]),
            (nums1[i] * nums2[j]) + Math.max(0, dp[i][j]));
      }
    }
    return dp[nums1Length][nums2Length];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/max-dot-product-of-two-subsequences/submissions/1070142738/){:target="_blank"}

# 설명
1. nums1의 임의 위치에서 nums2와의 [스칼라곱](https://en.wikipedia.org/wiki/Dot_product){:target="_blank"}이 최댓값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums1Length와 nums2Length은 nums1과 nums2의 길이를 저장한 변수이다.
- dp는 최댓값을 구하기 위한 배열로, $(nums1Length + 1) \times (nums2Length + 1)$ 크기의 2차원 정수 배열로 초기화하고 모든 값에 정수의 가장 작은 값을 넣어준다.

3. 0부터 nums1Length 미만까지 i를 증가시키고, 0부터 nums2Length 미만까지 j를 증가시키며 아래를 반복한다.
- dp[$i + 1$][$j + 1$] 위치에 아래의 값들 중 큰 값을 넣어준다.
  - dp[i][$j + 1$]의 값과 dp[$i + 1$][j]의 값 중 큰 값.
  - $nums1[i] \times nums2[j]$의 값에 이전 값이 존재하면 dp[i][j]를 아니면 0을 더한 값.

4. 반복이 완료되면 최댓값이 저장된 dp[nums1Length][nums2Length]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxDotProductOfTwoSubsequences.java){:target="_blank"}에서 확인 가능합니다.