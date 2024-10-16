---
title: "Leetcode Java Interleaving String"
excerpt: "Leetcode Interleaving String Java 풀이"
last_modified_at: 2021-07-17T20:00:00
header:
  image: /assets/images/leetcode/interleaving-string.png
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
[Link](https://leetcode.com/problems/interleaving-string/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isInterleave(String s1, String s2, String s3) {
    if ((s1.length() + s2.length()) != s3.length()) {
      return false;
    }
    boolean[][] dp = new boolean[s1.length() + 1][s2.length() + 1];
    dp[0][0] = true;
    for (int i = 1; i < dp.length; i++) {
      dp[i][0] = dp[i - 1][0] && (s1.charAt(i - 1) == s3.charAt(i - 1));
    }
    for (int i = 1; i < dp[0].length; i++) {
      dp[0][i] = dp[0][i - 1] && (s2.charAt(i - 1) == s3.charAt(i - 1));
    }
    for (int i = 1; i < dp.length; i++) {
      for (int j = 1; j < dp[0].length; j++) {
        dp[i][j] = (dp[i - 1][j] && (s1.charAt(i - 1) == s3.charAt(i + j - 1)))
            || (dp[i][j- 1] && (s2.charAt(j - 1) == s3.charAt(i + j - 1)));
      }
    }
    return dp[s1.length()][s2.length()];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/523855630/){:target="_blank"}

# 설명
1. 주어진 문자열 s1과 s2를 이용하여 s3를 만들 수 있는지 검증하는 문제이다.

2. 기본적으로 주어진 문자열 s1과 s2의 길이의 합이 주어진 문자열 s3와 같지 않으면, false를 문제의 결과로 반환한다.

3. 변수 dp를 주어진 변수 s1과 s2의 길이보다 하나 더 큰 사이즈로 정의하고, dp[0][0]을 true로 초기화 한다.
- dp의 첫 열을 s1의 길이만큼 반복하여 dp[$i - 1$][0]이 true이면서, s1와 s3의 $i - 1$번째 단어가 동일한지 확인한다.
- dp의 첫 행을 s2의 길이만큼 반복하여 dp[][$i - 1$]이 true이면서, s2와 s3의 $i - 1$번째 단어가 동일한지 확인한다.

4. dp를 반복하여 주어진 문자열 s1과 s2를 이용하여 s3를 만들 수 있는지 확인하며 dp를 채워준다.
- dp[i][j]에 dp[$i - 1$][j]의 값이 true이고 s1의 $i - 1$번째 자리와 s3의 $i + j - 1$번째 자리가 동일하거나, dp[i][$j - 1$]의 값이 true이고 s2의 $j - 1$번째 자리와 s3의 $i + j - 1$번째 자리가 동일한 경우 true를 넣고 아닌 경우 false를 넣어준다.

5. 반복이 완료되면 주어진 문자열 s1과 s2를 이용하여 s3를 만들 수 있는지의 결과를 저장한 dp[s1.length()][s2.length()]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InterleavingString.java){:target="_blank"}에서 확인 가능합니다.