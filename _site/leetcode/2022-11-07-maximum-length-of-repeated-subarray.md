---
title: "Leetcode Java 1-bit and 2-bit Characters"
excerpt: "Leetcode 1-bit and 2-bit Characters Java"
last_modified_at: 2022-11-07T18:10:00
header:
  image: /assets/images/leetcode/maximum-length-of-repeated-subarray.png
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
[Link](https://leetcode.com/problems/maximum-length-of-repeated-subarray){:target="_blank"}

# 코드
```java
class Solution {

  public int findLength(int[] nums1, int[] nums2) {
    int nums1Length = nums1.length;
    int nums2Length = nums2.length;
    int[][] dp = new int[nums1Length + 1][nums2Length + 1];
    int max = 0;
    for (int i = 0; i < nums1Length; i++) {
      for (int j = 0; j < nums2Length; j++) {
        if (nums1[i] == nums2[j]) {
          dp[i + 1][j + 1] = dp[i][j] + 1;
          max = Math.max(max, dp[i + 1][j + 1]);
        }
      }
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/838597570/){:target="_blank"}

# 설명
1. num1과 num2에 동시에 포함되는 부분 배열의 최대 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums1Length와 nums2Length는 nums1과 nums2의 길이를 각각 저장한 변수이다.
- dp는 num1과 num2에 동시에 포함되는 부분 배열의 최대 길이를 구하기 위한 변수로, [$nums1Length + 1$][$nums2Length + 1$] 크기의 2차원 배열로 초기화한다.
- max는 num1과 num2에 동시에 포함되는 부분 배열의 최대 길이를 저장하기 위한 변수로, 0으로 초기화한다.

3. 0부터 nums1Length 미만까지 i를 증가시키고, 0부터 nums2Length 미만까지 j를 증가시키며 아래를 반복 수행한다.
- num1[i]의 값과 num2[j]의 값이 동일한 경우, 아래를 수행한다.
  - dp[$i + 1$][$j + 1$]의 자리에 dp[i][j]의 값에 1을 더해 연속된 부분 배열의 길이를 저장한다.
  - max에 max와 위에서 계산된 부분 배열의 길이인 dp[$i + 1$][$j + 1$] 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 num1과 num2에 동시에 포함되는 부분 배열의 최대 길이를 저장한 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumLengthOfRepeatedSubarray.java){:target="_blank"}에서 확인 가능합니다.