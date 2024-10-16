---
title: "Leetcode Java Wildcard Matching"
excerpt: "Leetcode Wildcard Matching Java 풀이"
last_modified_at: 2021-05-26T17:00:00
header:
  image: /assets/images/leetcode/wildcard-matching.png
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
[Link](https://leetcode.com/problems/wildcard-matching/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isMatch(String s, String p) {
    boolean[][] dp = this.initDp(s, p);
    for (int i = 1; i < s.length() + 1; i++) {
      for (int j = 1; j < p.length() + 1; j++) {
        if (s.charAt(i - 1) == p.charAt(j - 1) || p.charAt(j - 1) == '?') {
          dp[i][j] = dp[i - 1][j - 1];
        } else if (p.charAt(j - 1) == '*') {
          dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
        } else {
          dp[i][j] = false;
        }
      }
    }
    return dp[s.length()][p.length()];
  }
  
  private boolean[][] initDp(String s, String p) {
    boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
    dp[0][0] = true;
    for (int idx = 1; idx < p.length() + 1; idx++) {
      if (p.charAt(idx - 1) == '*') {
        dp[0][idx] = dp[0][idx - 1];
      }
    }
    return dp;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/498352383/){:target="_blank"}

# 설명
1. 주어진 문자열 p의 패턴 기반으로 s가 일치하는지를 검증하기 위하여 배열 dp를 \[$s.length() + 1$\]\[$p.length() + 1$\]의 크기로 정의 한다.

2. 초기 dp[0][0]은 true로 하여, 패턴의 길이만큼 반복하여 배열 dp를 초기화 한다.
- 만일, 패턴의 문자가 '*'인 경우 모든 문자가 들어가도 상관 없으므로 dp[0]\[$idx - 1$\]의 값을 dp[0][idx]에 넣어준다.
- 그 외의 값은 boolean의 기본 값인 false로 들어가게 된다.

3. 초기화된 배열 dp를 이용하여 반복문을 통해 문자열과 비교를 한다.
- 주어진 문자열 s의 $i - 1$번째 자리와 p의 $j - 1$번째 자리와 같으면 동일 문자열이고, '?'이면 단일 임의 문자와 일치하므로 dp[i][j]의 값에 직전 대각의 값인 dp\[$i - 1$\]\[$j - 1$\]을 주입한다.
- 주어진 문자열 p의 $j - 1$번째 자리가 '*'인 경우, dp[i][j]의 값에 기 검증된 dp\[$i - 1$\][j] OR dp[i]\[$j - 1$\]의 결과를 주입한다.
- 그 외의 경우엔 dp[i][j]에 false를 주입한다.

4. 반복이 완료되면 주어진 문자열 p의 패턴과 s가 일치하는지의 결과인 dp[s.length()][p.length()]값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WildcardMatching.java){:target="_blank"}에서 확인 가능합니다.