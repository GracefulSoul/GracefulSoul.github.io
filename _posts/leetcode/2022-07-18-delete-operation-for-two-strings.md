---
title: "Leetcode Java Delete Operation for Two Strings"
excerpt: "Leetcode Delete Operation for Two Strings Java"
last_modified_at: 2022-07-18T19:30:00
header:
  image: /assets/images/leetcode/delete-operation-for-two-strings.png
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
[Link](https://leetcode.com/problems/delete-operation-for-two-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public int minDistance(String word1, String word2) {
    int word1Length = word1.length();
    int word2Length = word2.length();
    char[] word1CharArray = word1.toCharArray();
    char[] word2CharArray = word2.toCharArray();
    int dp[][] = new int[word1Length + 1][word2Length + 1];
    for (int i = 0; i <= word1Length; i++) {
      for (int j = 0; j <= word2Length; j++) {
        if (i == 0 || j == 0) {
          dp[i][j] = 0;
        } else {
          dp[i][j] = (word1CharArray[i - 1] == word2CharArray[j - 1]) ? dp[i - 1][j - 1] + 1 : Math.max(dp[i - 1][j], dp[i][j - 1]);
        }
      }
    }
    return word1Length + word2Length - (2 * dp[word1Length][word2Length]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/750147526/){:target="_blank"}

# 설명
1. word1과 word2를 동일하게 만들기 위한 최소 횟수를 구하는 문제이다.
- 단, 한 단계에서 두 문자열 중 한 문자만 삭제할 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- word1Length, word2Length는 word1과 word2 길이를 저장한 변수이다.
- word1CharArray, word2CharArray는 word1과 word2의 문자 배열을 변환하여 저장한 변수이다.
- dp는 두 문자를 동일하게 만들기 위한 최소 횟수를 구하기 위한 배열로, $(word1Length + 1) \times (word2Length + 1)$ 크기로 초기화한다.

3. 0부터 word1Length 이하까지 i를 증가하며, 0부터 word2Length를 증가하면 아래를 반복한다.
- i 혹은 j가 0인 경우, dp[i][j]에 0을 넣어 초기화한다.
- 그 외의 경우 dp[i][j]에 word1CharArray[$i - 1$]의 문자와 word2CharArray[$j - 1$]의 문자가 동일하면 해당 단어를 삭제하지 않아도 되므로 대각선 상 존재하는 dp[i - 1][j - 1]의 값에 1을 더한 값을, 아니면 이전 값들인 dp[$i - 1$][j]의 값과 dp[i][$j - 1$] 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 word1Length과 word2Length를 더한 값에 dp[word1Length][word2Length] 값의 2배를 뺀 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteOperationForTwoStrings.java){:target="_blank"}에서 확인 가능합니다.