---
title: "Leetcode Java Ones and Zeroes"
excerpt: "Leetcode Ones and Zeroes Java 풀이"
last_modified_at: 2022-04-30T18:00:00
header:
  image: /assets/images/leetcode/ones-and-zeroes.png
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
[Link](https://leetcode.com/problems/ones-and-zeroes/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMaxForm(String[] strs, int m, int n) {
    int[][] dp = new int[m + 1][n + 1];
    for (String s : strs) {
      int[] count = new int[2];
      for (char c : s.toCharArray()) {
        if (c == '0') {
          count[0]++;
        } else {
          count[1]++;
        }
      }
      for (int i = m; i >= count[0]; i--) {
        for (int j = n; j >= count[1]; j--) {
          dp[i][j] = Math.max(dp[i][j], 1 + dp[i - count[0]][j - count[1]]);
        }
      }
    }
    return dp[m][n];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/690123202/){:target="_blank"}

# 설명
1. 이진수로 이루어진 문자열의 배열인 strs 내 m개의 0과 n개의 1로 구성할 수 있는 부분 집합의 최대 개수를 구하는 문제이다.

2. dp를 $m + 1$과 $n + 1$ 크기로 정의한다.

3. strs의 모든 값들을 반복하여 아래를 수행한다.
- count 배열을 2 크기로 정의하여 0과 1의 개수를 각각 넣어준다.
- m부터 count[0]까지 i를 감소시키고, n부터 count[1]까지 j를 감소시키며 반복을 수행한다.
  - dp[i][j]의 값에 dp[i][j]와 dp[$i - count[0]$][$j - count[1]$]에 1을 더한 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 부분 집합의 최대 개수인 dp[m][n]를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OnesAndZeroes.java){:target="_blank"}에서 확인 가능합니다.