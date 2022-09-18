---
title: "Leetcode Java Strange Printer"
excerpt: "Leetcode Strange Printer Java"
last_modified_at: 2022-09-18T11:30:00
header:
  image: /assets/images/leetcode/strange-printer.png
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
[Link](https://leetcode.com/problems/strange-printer){:target="_blank"}

# 코드
```java
class Solution {

  public int strangePrinter(String s) {
    int length = s.length();
    int[][] dp = new int[length][length];
    for (int idx = 0; idx < length; idx++) {
      dp[idx][idx] = 1;
      if (idx + 1 < length) {
        dp[idx][idx + 1] = s.charAt(idx) == s.charAt(idx + 1) ? 1 : 2;
      }
    }
    for (int l = 3; l <= length; l++) {
      for (int i = 0; i <= length - l; i++) {
        int j = i + l - 1;
        dp[i][j] = Integer.MAX_VALUE;
        for (int k = i; k < j; k++) {
          dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k + 1][j]);
        }
        if (s.charAt(i) == s.charAt(j)) {
          dp[i][j]--;
        }
      }
    }
    return dp[0][length - 1];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/802475396/){:target="_blank"}

# 설명
1. s의 문자열을 이용하여 아래의 조건을 만족하는 프린터의 최소 출력 횟수를 구하는 문제이다.
- 프린터는 매 번 동일한 문자의 시퀀스만 인쇄할 수 있다.
- 각 출력은 임의 위치에서 시작하고 끝나는 문자를 인쇄할 수 있으며, 기존 문자를 덮을 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 s의 길이를 저장한 변수이다.
- dp는 최소 출력 횟수를 구하기 위한 배열로, $length \times length$ 크기로 초기화한다.

3. dp의 대각선 위치에 1을 넣고, 그 오른쪽 위치에 각 위치 문자가 동일한 경우 1을 아니면 2를 넣어준다.

4. 3부터 length 이하까지 l을 증가시키고, 0부터 $length - l$ 이하까지 i를 증가시키며 아래를 수행한다.
- j에 $i + l - 1$을 넣어준다.
- dp[i][j]에 정수 최댓값을 넣어주고, i부터 j 미만까지 k를 증가시키며 dp[i][j]와 $dp[i][k] + dp[k + 1][j]$ 중 작은 값을 dp[i][j]에 넣어 최소 횟수를 탐색한다.
- s의 i번째 문자와 j번째 문자가 동일한 경우 같은 출력 횟수에 포함 가능하므로, dp[i][j]를 감소시킨다.

5. 반복이 완료되면 최소 횟수인 dp[0][$length - 1$]을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StrangePrinter.java){:target="_blank"}에서 확인 가능합니다.