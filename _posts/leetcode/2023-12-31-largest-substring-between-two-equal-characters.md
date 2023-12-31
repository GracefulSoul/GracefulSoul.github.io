---
title: "Leetcode Java Largest Substring Between Two Equal Characters"
excerpt: "Leetcode Largest Substring Between Two Equal Characters Java"
last_modified_at: 2023-12-31T10:45:00
header:
  image: /assets/images/leetcode/largest-substring-between-two-equal-characters.png
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
[Link](https://leetcode.com/problems/largest-substring-between-two-equal-characters){:target="_blank"}

# 코드
```java
class Solution {

  public int maxLengthBetweenEqualCharacters(String s) {
    int[] dp = new int[26];
    int max = -1;
    for (int i = 0; i < s.length(); i++) {
      int index = s.charAt(i) - 97;
      if (dp[index] == 0) {
        dp[index] = i + 1;
      } else {
        max = Integer.max(max, i - dp[index]);
      }
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-substring-between-two-equal-characters/submissions/1132603544/){:target="_blank"}

# 설명
1. 문자열 s의 동일한 두 문자의 길이가 가장 긴 구간을 찾는 문제이다.
- 단, 동일한 문자가 없으면 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 문자의 시작 위치를 저장할 변수로, 영문자의 갯수인 26 크기의 정수 배열로 초기화한다.
- max는 가장 긴 길이를 저장할 변수로 -1로 초기화한다.

3. 0부터 s의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- index에 s의 i번째 문자 위치의 값을 저장한다.
- dp[index]의 값이 존재하지 않는 경우, $i + 1$을 넣어준다.
- dp[index]의 값이 존재하는 경우, max에 max와 $i - dp[index]$의 값을 넣어 가장 긴 길이를 저장한다.

4. 반복이 완료되면 가장 긴 길이가 저장된 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestSubstringBetweenTwoEqualCharacters.java){:target="_blank"}에서 확인 가능합니다.