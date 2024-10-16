---
title: "Leetcode Java Shortest Common Supersequence"
excerpt: "Leetcode Shortest Common Supersequence Java"
last_modified_at: 2024-04-23T18:50:00
header:
  image: /assets/images/leetcode/shortest-common-supersequence.png
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
[Link](https://leetcode.com/problems/shortest-common-supersequence/){:target="_blank"}

# 코드
```java
class Solution {

  public String shortestCommonSupersequence(String str1, String str2) {
    int str1Length = str1.length();
    int str2Length = str2.length();
    char[] str1CharArray = str1.toCharArray();
    char[] str2CharArray = str2.toCharArray();
    int[][] dp = new int[str1Length + 1][str2Length + 1];
    for (int i = str1Length - 1; i >= 0; i--) {
      for (int j = str2Length - 1; j >= 0; j--) {
        if (str1CharArray[i] == str2CharArray[j]) {
          dp[i][j] = 1 + dp[i + 1][j + 1];
        } else {
          dp[i][j] = Math.max(dp[i + 1][j], dp[i][j + 1]);
        }
      }
    }
    StringBuilder sb = new StringBuilder();
    for (int i = 0, j = 0; i < str1Length || j < str2Length;) {
      if (i < str1Length ^ j < str2Length) {
        sb.append(i < str1Length ? str1CharArray[i++] : str2CharArray[j++]);
      } else if (str1CharArray[i] == str2CharArray[j]) {
        sb.append(str1CharArray[i++]);
        ++j;
      } else {
        sb.append(dp[i + 1][j] > dp[i][j + 1] ? str1CharArray[i++] : str2CharArray[j++]);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shortest-common-supersequence/submissions/1239768789/){:target="_blank"}

# 설명
1. str1과 str2가 모두 포함되는 문자열 중 가장 짧은 문자열을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- str1Length와 str2Length는 str1과 str2의 길이를 각각 저장한 변수이다.
- str1CharArray와 str2CharArray는 str1과 str2를 각각 문자 배열로 변환한 변수이다.
- dp는 문자열 조합에 가능한 길이를 저장할 변수로, $(str1Length + 1) \times (str2Length + 1)$ 길이의 2차원 배열로 초기화한다.

3. $str1Length - 1$부터 0까지 i를 감소시키고 $str2Length - 1$부터 0까지 j를 감소시키며 아래를 반복한다.
- str1CharArray[i]의 값과 str2CharArray[j]의 값이 동일하면 dp[i][j]의 위치에 $1 + dp[i + 1][j + 1]$를 넣어 합쳐지는 문자열의 길이를 증가시킨다.
- 위의 경우가 아니라면 dp[i][j]의 위치에 $dp[i + 1][j]$의 값과 $dp[i][j + 1]$의 값 중 큰 가장 긴 길이의 문자열의 길이를 넣어준다.

4. sb는 문자열을 동적으로 만들기 위한 변수로, StringBuilder로 초기화한다.

5. i와 j가 0부터 i가 str1Length 미만이거나 j가 str2Length미만일 때 까지 아래를 반복한다.
- i가 str1Length보다 작은 결과와 j가 str2Length보다 작은 결과의 XOR(^) 연산의 결과가 참인 경우, i가 str1Length보다 작으면 sb에 str1CharArray[i]의 값을 넣고 i를 증가시키고 아니면 sb에 str2CharArray[j]의 값을 넣고 j를 증가시킨다.
- 위의 경우가 아니면서 str1CharArray[i]의 값과 str2CharArray[j]의 값이 동일한 경우, sb에 str1CharArray[i]를 넣고 i를 증가시킨다.
- 그 외의 경우 sb에 dp[i + 1][j]의 값이 dp[i][j + 1]의 값보다 크면, str1CharArray[i]의 값을 넣고 i를 증가시키고 아니면 sb에 str2CharArray[j]의 값을 넣고 j를 증가시킨다.

6. 반복이 완료되면 완성된 결과인 sb를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestCommonSupersequence.java){:target="_blank"}에서 확인 가능합니다.