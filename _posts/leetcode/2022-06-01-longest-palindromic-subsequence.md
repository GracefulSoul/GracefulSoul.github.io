---
title: "Leetcode Java Longest Palindromic Subsequence"
excerpt: "Leetcode - 'Longest Palindromic Subsequence' 문제 Java 풀이"
last_modified_at: 2022-06-01T12:00:00
header:
  image: /assets/images/leetcode/longest-palindromic-subsequence.png
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
[Link](https://leetcode.com/problems/longest-palindromic-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestPalindromeSubseq(String s) {
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    int max = 0;
    int[] dp = new int[length];
    for (int j = 0; j < length; j++) {
      dp[j] = 1;
      max = 0;
      for (int i = j - 1; i >= 0; i--) {
        int len = dp[i];
        if (charArray[i] == charArray[j]) {
          dp[i] = 2 + max;
        }
        max = Math.max(max, len);
      }
    }
    for (int len : dp) {
      max = Math.max(max, len);
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/711659468/){:target="_blank"}

# 설명
1. 문자열의 앞과 끝을 이어 원형으로 구성했을 경우, 부분 문자열 중 가장 긴 반복되는 단어의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s의 문자를 배열로 전환해서 저장할 변수이다.
- length는 s의 길이인 charArray의 길이를 저장할 변수이다.
- max는 최댓값을 저장하기 위한 변수이다.
- dp는 길이를 추정하기 위한 배열을 저장하기 위한 배열로, length 크기로 정의한다.

3. 0부터 length 미만까지 j를 증가시키며 반복을 수행한다.
- dp의 j번째 위치에 1으로, max를 0으로 초기화한다.
- $j - 1$부터 0까지 i를 감소시키며 역순으로 탐색을 수행한다.
  - len에 dp의 i번째 값을 보관해준다.
  - charArray의 i번쨰 값과 j번째 값이 동일한 경우 두 단어가 동일하므로, dp의 i번째 위치에 $2 + max$를 넣어준다.
  - max에 max와 len 중 큰 값을 넣어준다.

4. 반복이 완료되면 dp를 반복하여 max와 dp의 값중 가장 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestPalindromicSubsequence.java){:target="_blank"}에서 확인 가능합니다.