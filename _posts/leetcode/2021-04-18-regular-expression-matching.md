---
title: "Leetcode Java Regular Expression Matching"
excerpt: "Leetcode Regular Expression Matching Java 풀이"
last_modified_at: 2021-04-17T12:50:00
header:
  image: /assets/images/leetcode/regular-expression-matching.png
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
[Link](https://leetcode.com/problems/regular-expression-matching/){:target="_blank"}

# 코드
```java
class Solution {

	public boolean isMatch(String s, String p) {
		if (isBlank(p)) {
			return isBlank(s);
		}
		boolean[][] dp = initDp(s, p);
		for (int i = 0; i < s.length(); i++) {
			for (int j = 0; j < p.length(); j++) {
				if (p.charAt(j) == '.' || p.charAt(j) == s.charAt(i)) {
					dp[i + 1][j + 1] = dp[i][j];
				} else if (p.charAt(j) == '*') {
					if (p.charAt(j - 1) != s.charAt(i) && p.charAt(j - 1) != '.') {
						dp[i + 1][j + 1] = dp[i + 1][j - 1];
					} else {
						dp[i + 1][j + 1] = (dp[i + 1][j] || dp[i][j + 1] || dp[i + 1][j - 1]);
					}
				}
			}
		}
		return dp[s.length()][p.length()];
	}

	private boolean isBlank(String s) {
		return s == null || s.length() == 0;
	}

	private boolean[][] initDp(String s, String p) {
		boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
		dp[0][0] = true;
		for (int i = 1; i < p.length(); i+=2) {
			dp[0][i + 1] = p.charAt(i) == '*' && dp[0][i - 1];
		}
		return dp;
	}

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/481648922/){:target="_blank"}

# 설명
1. 주어진 패턴 p가 null이거나 길이가 0이라면 주어진 문자열 s가 null이거나 길이가 0인지를 주어진 문제의 결과로 반환한다.
	- 패턴이 없을 경우 문자열도 없어야 정상이기 때문이다.

2. 해당 문제를 주어진 문자열 s와 주어진 패턴 p를 활용하기 위해 2차원 boolean 배열인 dp에 주어진 패턴 p의 '*'이 들어가 있는 위치를 먼저 설정한다.
	- 주어진 패턴 p를 이용하여 초기 값인 dp[0][0]의 값을 true로 설정한다.
	- 주어진 패턴 p의 i번째 문자가 '*'이고 dp[0][i - 1]의 값이 true일 경우, dp[0][i + 1]의 값을 true로 설정한다.
	- 문자가 '*'이 들어가는 위치는 특정 문자열 뒤에 붙으므로, 짝수열만 탐색하면 되어 i는 1부터 2씩 증가시킨다.

3. 주어진 문자열 s와 주어진 패턴 p를 각각 비교하기 위해 s와 p의 길이만큼 각각 반복을 수행한다.
	- 만일 주어진 패턴의 j번째 문자가 '.'이거나, 주어진 패턴의 j번째 문자와 주어진 문자열 s의 i번째 자리가 동일한 경우 dp[i + 1][j + 1]의 값에 dp[i][j]의 값을 주입한다.
		- 위의 경우는 해당 문자열이 임의 문자가 들어가거나, 동일 문자가 들어가는 경우이므로, 해당 위치까지 주어진 문자열이 주어진 패턴에 부합하다고 판단한다.
	- 만일 주어진 패턴의 j번째 문자가 '*'인 경우, 아래의 조건 확인한다.
		- 주어진 패턴의 j - 1번째 문자가 주어진 문자열의 i번째 문자와 다르고 주어진 패턴의 j - 1번째 문자가 '.'이 아닌 경우, dp[i + 1][j + 1]의 값에 dp[i + 1][j - 1]의 값을 주입한다.
		- 위의 경우가 아닌 경우, dp[i + 1][j + 1]의 값에 아래의 조건에 부합하는 경우 true, 하나도 부합하지 않는 경우 false로 설정한다.
			- dp[i + 1][j]의 값이 true
			- dp[i][j + 1]의 값이 true
			- dp[i + 1][j - 1])의 값이 true

4. 반복이 끝난 경우 dp[s.length()][p.length()]의 값을 주어진 문제의 결과로 반환한다.
	- dp 배열의 s의 길이, p의 길이 위치에 있는 값은 주어진 문자열이 주어진 패턴에 부합한다고 판단되는 경우이기 때문에, 해당 값이 문제의 결과이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PalindromeNumber.java){:target="_blank"}에서 확인 가능합니다.