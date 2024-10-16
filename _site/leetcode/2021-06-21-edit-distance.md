---
title: "Leetcode Java Edit Distance"
excerpt: "Leetcode Edit Distance Java 풀이"
last_modified_at: 2021-06-21T17:40:00
header:
  image: /assets/images/leetcode/edit-distance.png
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
[Link](https://leetcode.com/problems/edit-distance/){:target="_blank"}

# 코드
```java
class Solution {

  public int minDistance(String word1, String word2) {
    int[][] dp = this.initDp(word1.length(), word2.length());
    for (int i = 0; i < word1.length(); i++) {
      for (int j = 0; j < word2.length(); j++) {
        if (word1.charAt(i) == word2.charAt(j)) {
          dp[i + 1][j + 1] = dp[i][j];
        } else {
          dp[i + 1][j + 1] = 1 + Math.min(dp[i][j], Math.min(dp[i][j + 1], dp[i + 1][j]));
        }
      }
    }
    return dp[word1.length()][word2.length()];
  }
  
  private int[][] initDp(int len1, int len2) {
    int[][] dp = new int[len1 + 1][len2 + 1];
    for (int i = 0; i < len1; i++) {
      dp[i + 1][0] = i + 1;
    }
    for (int j = 0; j < len2; j++) {
      dp[0][j + 1] = j + 1;
    }
    return dp;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/510970148/){:target="_blank"}

# 설명
1. 주어진 문자열 word1으로 각 문자를 추가/수정/삭제하여 word2로 만들기 위한 최소 횟수를 구하는 문제이다.

2. 문자열 word1을 word2로 변환하기 위한 횟수를 저장할 DP를 초기화 한다.
- DP는 word1과 word2의 각 길이 + 1만큼으로 정의한다.
- 초기 DP[0][0]은 0으로 시작하여 0번째 행과 열은 각 문자열까지의 길이로 초기화 한다.

3. 2번으로 초기화 한 DP를 이용하여 초기화된 0번째 행과 열을 제외한 모든 자리를 반복하여 word1을 word2로 만들기 위한 최소 횟수를 구한다.
- word1의 i 번째 문자와 word2의 j 번째 문자가 동일하면 해당 문자를 변경하지 않아도 되므로, dp[i + 1][j + 1]의 값에 dp[i][j] 값을 넣어준다.
- word1의 i 번째 문자와 word2의 j 번째 문자가 동일하지 않다면 해당 문자를 변경해야 하므로, dp[i + 1][j + 1]의 값에 해당 셀의 좌측, 좌측 상단 대각선, 상단의 값 중 가장 작은 값으로 넣어준다.

4. 3번으로 완성된 DP의 마지막 값인 DP[word1.length()][word2.length()]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EditDistance.java){:target="_blank"}에서 확인 가능합니다.