---
title: "Leetcode Java Distinct Subsequences"
excerpt: "Leetcode Distinct Subsequences Java 풀이"
last_modified_at: 2021-08-05T23:20:00
header:
  image: /assets/images/leetcode/distinct-subsequences.png
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
[Link](https://leetcode.com/problems/distinct-subsequences/){:target="_blank"}

# 코드
```java
class Solution {

  public int numDistinct(String s, String t) {
    int[][] dp = this.initDp(s.length(), t.length());
    for (int j = 1; j < t.length() + 1; j++) {
      for (int i = 1; i < s.length() + 1; i++) {
        dp[i][j] = dp[i - 1][j];
        if (s.charAt(i - 1) == t.charAt(j - 1)) {
          dp[i][j] += dp[i - 1][j - 1];
        }
      }
    }
    return dp[s.length()][t.length()];
  }

  private int[][] initDp(int row, int col) {
    int[][] dp = new int[row + 1][col + 1];
    for (int i = 0; i < row + 1; i++) {
      dp[i][0] = 1;
    }
    return dp;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/533736857/){:target="_blank"}

# 설명
1. 주어진 문자열 s의 각 문자열을 이용하여 문자열 t를 몇 개 만들수 있는지 경우의 수를 구하는 문제이다.

2. DP를 s와 t의 길이보다 하나 더 크게 만들어주고, 첫 열을 1로 초기화 해준다.

3. 주어진 문자열 s와 t의 길이만큼 반복하여 dp를 만들어준다.
- dp[i][j]에 윗 행의 값인 dp[$i - 1$][j]의 값을 넣어준다.
- 주어진 문자열 s의 $i - 1$번째 문자와 t의 $j - 1$번째 값이 동일하면 대각선의 위치인 dp[$i - 1$][$j - 1$] 값을 추가해준다.

4. 완성된 DP의 dp[s.length()][t.length()] 값은 주어진 문자열 s를 이용하여 t를 만들 수 있는 경우의 수를 나타내므로, 이 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DistinctSubsequences.java){:target="_blank"}에서 확인 가능합니다.