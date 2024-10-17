---
title: "Leetcode Java Longest Common Subsequence"
excerpt: "Leetcode Medium - 'PseuLongest Common Subsequence' 문제 Java 풀이"
last_modified_at: 2024-01-25T19:00:00
header:
  image: /assets/images/leetcode/longest-common-subsequence.png
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
[Link](https://leetcode.com/problems/longest-common-subsequence){:target="_blank"}

# 코드
```java
class Solution {

	public int longestCommonSubsequence(String text1, String text2) {
		char[] text1CharArray = text1.toCharArray();
		char[] text2CharArray = text2.toCharArray();
		int text1Length = text1CharArray.length;
		int text2Length = text2CharArray.length;
		int[][] dp = new int[text1Length + 1][text2Length + 1];
		for (int i = 1; i <= text1Length; i++) {
			for (int j = 1; j <= text2Length; j++) {
				if (text1CharArray[i - 1] == text2CharArray[j - 1]) {
					dp[i][j] = 1 + dp[i - 1][j - 1];
				} else {
					dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
				}
			}
		}
		return dp[text1Length][text2Length];
	}

}
```

# 결과
[Link](https://leetcode.com/problems/longest-common-subsequence/submissions/1156390889/){:target="_blank"}

# 설명
1. text1과 text2의 중간 문자들만 제거하여 동일하게 만들 수 있는 가장 긴 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- text1CharArray와 text2CharArray는 text1과 text2를 문자 배열로 변환하여 저장한 변수이다.
- text1Length와 text2Length는 text1과 text2의 문자 길이를 저장한 변수이다.
- dp는 가장 긴 문자열의 길이를 찾기 위한 배열로, $(text1Length + 1) \times (text2Length + 1)$ 크기의 2차원 배열로 초기화한다.

3. 1부터 text1Length 이하까지 i를 증가시키고, 1부터 text2Length 이하까지 j를 증가시키며 아래를 반복한다.
- text1CharArray[$i - 1$] 문자와 text2CharArray[$j - 1$] 문자가 동일한 경우, dp[i][j]에 현재까지 위치를 추가하여 $1 + dp[i - 1][j - 1]$의 값을 넣어준다.
- 위의 경우가 아닌 경우, 이전 위치까지 각 경우인 dp[i][j]에 dp[$i - 1$][j]와 dp[i][$j - 1$] 중 큰 값을 넣어준다.

4. 반복이 완료되면 가장 긴 길이가 저장된 dp[text1Length][text2Length]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestCommonSubsequence.java){:target="_blank"}에서 확인 가능합니다.