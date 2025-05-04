---
title: "Leetcode Java Scramble String"
excerpt: "Leetcode - 'Scramble String' 문제 Java 풀이"
last_modified_at: 2025-05-04T20:10:00
header:
  image: /assets/images/leetcode/scramble-string.png
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
[Link](https://leetcode.com/problems/scramble-string/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isScramble(String s1, String s2) {
    int length = s1.length();
    boolean[][][] dp = new boolean[length][length][length + 1];
    for (int k = 1; k <= length; k++) {
      for (int i = 0; i + k <= length; i++) {
        for (int j = 0; j + k <= length; j++) {
          if (k == 1) {
            dp[i][j][k] = s1.charAt(i) == s2.charAt(j);
          } else {
            for (int l = 1; l < k && !dp[i][j][k]; l++) {
              dp[i][j][k] = (dp[i][j][l] && dp[i + l][j + l][k - l]) || (dp[i][j + k - l][l] && dp[i + l][j][k - l]);
            }
          }
        }
      }
    }
    return dp[0][0][length];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/scramble-string/submissions/1625203618/){:target="_blank"}

# 설명
1. 문자열 s1을 아래 알고리즘에 따라 s2로 변환이 가능한지 검증하는 문제이다.
- 문자열의 길이가 1인 경우 알고리즘을 수행할 수 없으며, 1 초과인 경우만 알고리즘을 수행할 수 있다.
- 문자열을 임의 부분 문자열로 분할 후 두 문자열의 순서를 교체하거나 그대로 유지할 수 있다.
- 위 두 단계를 재귀적으로 수행한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 s1의 길이를 저장한 변수이다.
- dp는 각 경우를 반복하여 검증하기 위한 배열로, $length \times length \times (length + 1)$ 크기의 3차원  정수 배열로 초기화한다.

3. 1부터 length 이하까지 k를 증가시키고, 0부터 $i + k$가 length 이하까지 i를 증가시키고, 0부터 $j + k$가 length 이하까지 j를 증가시키며 아래를 반복한다.
- k가 1인 경우 알고리즘을 수행할 수 없는 경우, dp[i][j][k]의 값에 s1의 i번째 문자와 s2의 j번째 문자가 동일한지 검증한다.
- k가 1 초과인 알고리즘을 수행하는 경우, l이 1부터 k 미만이면서 dp[i][j][k]의 값이 false일 때 까지 아래를 반복한다.
  - dp[i][j][k]의 위치에 dp[i][j][l]의 값과 dp[$i + l$][$j + l$][$k - l$]의 값이 모두 true이거나, dp[i][$j + k - l$][l]의 값과 dp[i + l][j][k - l]의 값이 모두 true인 둘 중 하나라도 만족하는 부분적으로 변환 가능하면 true를, 둘 다 만족하지 않아 변환할 수 없으면 false를 넣어준다.

4. 반복이 완료되면 dp[0][0][length]의 값인 변환 가능한지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ScrambleString.java){:target="_blank"}에서 확인 가능합니다.