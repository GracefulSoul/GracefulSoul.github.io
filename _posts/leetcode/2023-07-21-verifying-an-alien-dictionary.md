---
title: "Leetcode Java Verifying an Alien Dictionary"
excerpt: "Leetcode Verifying an Alien Dictionary Java"
last_modified_at: 2023-07-21T19:30:00
header:
  image: /assets/images/leetcode/verifying-an-alien-dictionary.png
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
[Link](https://leetcode.com/problems/verifying-an-alien-dictionary){:target="_blank"}

# 코드
```java
class Solution {

	private int[] point = new int[26];

	public boolean isAlienSorted(String[] words, String order) {
		for (int i = 0; i < order.length(); i++) {
			this.point[order.charAt(i) - 'a'] = i;
		}
		for (int i = 1; i < words.length; i++) {
			if (this.compare(words[i - 1], words[i])) {
				return false;
			}
		}
		return true;
	}

	private boolean compare(String s1, String s2) {
		int s1Lenth = s1.length();
		int s2Lenth = s2.length();
		for (int i = 0; i < s1Lenth && i < s2Lenth; i++) {
			if (s1.charAt(i) != s2.charAt(i)) {
				return this.point[s1.charAt(i) - 'a'] > this.point[s2.charAt(i) - 'a'];
			}
		}
		return s1Lenth > s2Lenth;
	}

}
```

# 결과
[Link](https://leetcode.com/problems/verifying-an-alien-dictionary/submissions/1000082177/){:target="_blank"}

# 설명
1. words의 붙어있는 두 문자열의 문자들이 order에 해당하는 사전 정렬 순으로 되어 있는지 검증하는 문제이다.

2. 전역 변수인 point는 order의 각 문자열 순서를 저장하기 위한 변수로, order의 모든 문자들을 반복하여 각 문자의 순서를 넣어준다.

3. 1부터 words의 길이 미만까지 i를 증가시키면서 아래를 반복한다.
- 4번에서 정의한 compare(String s1, String s2) 메서드에 words의 $i - 1$번째 문자와 i번째 문자의 결과가 true이면, 두 문자열의 오름차순 정렬이 아니므로 false를 주어진 문제의 결과로 반환한다.

4. 두 문자열의 비교를 위한 compare(String s1, String s2) 메서드를 정의한다.
- s1Length와 s2Length는 s1과 s2의 문자열 길이를 저장한 변수이다.
- 0부터 s1Length와 s2Length 미만일 때 까지 i를 증가시키며 아래를 반복한다.
  - s1과 s2의 i번째 문자의 값이 다른 경우 s1의 i번째 문자가 s2의 i번째 문자보다 order 내 순서가 뒤에 위치하는지 결과를 반환한다.
- 반복이 완료되면 s1의 길이가 s2의 길이보다 긴지 검증한 결과를 반환한다.

5. 반복이 완료되면 주어진 조건을 만족하므로 true를 주어진 문제의 결과로 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/VerifyingAnAlienDictionary.java){:target="_blank"}에서 확인 가능합니다.