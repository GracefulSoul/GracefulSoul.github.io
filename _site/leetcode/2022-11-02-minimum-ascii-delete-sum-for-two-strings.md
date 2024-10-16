---
title: "Leetcode Java Minimum ASCII Delete Sum for Two Strings"
excerpt: "Leetcode Minimum ASCII Delete Sum for Two Strings Java"
last_modified_at: 2022-11-02T19:40:00
header:
  image: /assets/images/leetcode/minimum-ascii-delete-sum-for-two-strings.png
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
[Link](https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumDeleteSum(String s1, String s2) {
    int s1Length = s1.length();
    int s2Length = s2.length();
    char[] s1CharArray = s1.toCharArray();
    char[] s2CharArray = s2.toCharArray();
    int s1Sum = 0;
    int s2Sum = 0;
    int[][] dp = new int[s1Length + 1][s2Length + 1];
    for (int i = 0; i < s1Length; i++) {
      s1Sum += s1CharArray[i];
      for (int j = 0; j < s2Length; j++) {
        if (i == 0) {
          s2Sum += s2CharArray[j];
        }
        dp[i + 1][j + 1] = s1CharArray[i] == s2CharArray[j] ? dp[i][j] + s1CharArray[i] : Math.max(dp[i][j + 1], dp[i + 1][j]);
      }
    }
    return s1Sum + s2Sum - (2 * dp[s1Length][s2Length]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/835302563/){:target="_blank"}

# 설명
1. 문자열 s1과 s2이 같아지기 위해 삭제한 문자의 ASCII 코드의 합이 가장 작은 결과를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- s1Length와 s2Length는 s1과 s2의 길이를 각각 저장한 변수이다.
- s1CharArray와 s2CharArray는 s1과 s2를 문자 배열로 각각 변환하여 저장한 변수이다.
- s1Sum과 s2Sum은 s1과 s2 각각 모든 문자의 ASCII 코드 합을 저장할 변수로 둘 다 0으로 초기화한다.
- dp는 s1과 s2가 같은 문자의 ASCII 코드 합이 가장 큰 값을 구할 변수로, [$s1Length + 1$][$s2Length + 1$] 크기의 2차원 정수 배열로 초기화 한다.

3. 0부터 s1Length까지 i를 증가시키며 아래를 수행한다.
- s1Sum에 s1CharArray의 i번쨰 값을 더해 s1의 모든 문자 ASCII 코드 합을 저장한다.
- 0부터 s2Length까지 j를 증가시키며 아래를 수행한다.
  - i가 0인 경우, s2Sum에 s2CharArray의 j번째 값을 더해 s2의 모든 문자 ASCII 코드 합을 저장한다.
  - s1CharArray의 i번째 문자와 s2CharArray의 j번째 문자가 동일한 경우, dp[$i + 1$][$j + 1$]에 dp[i][j]의 값에 공통된 문자의 ASCII 코드 값을 더한 값을 저장한다.
  - 위의 경우가 아니라면, dp[$i + 1$][$j + 1$]에 dp[i][$j + 1$]의 값과 dp[$i + 1$][j]의 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 s1Sum과 s2Sum의 합인 모든 문자의 ASCII 코드 값의 합에 s1과 s2의 공통된 문자의 ASCII 코드 값이 최대인 dp[s1Length][s2Length]값의 2배를 뺀 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumASCIIDeleteSumForTwoStrings.java){:target="_blank"}에서 확인 가능합니다.