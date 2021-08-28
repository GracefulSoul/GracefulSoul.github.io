---
title: "Leetcode Java Word Break"
excerpt: "Leetcode Word Break Java 풀이"
last_modified_at: 2021-08-27T12:00:00
header:
  image: /assets/images/leetcode/word-break.png
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
[Link](https://leetcode.com/problems/word-break/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean wordBreak(String s, List<String> wordDict) {
    boolean[] dp = new boolean[s.length() + 1];
    Set<String> wordSet = new HashSet<>();
    wordSet.addAll(wordDict);
    dp[0] = true;
    for (int i = 1; i <= s.length(); i++) {
      for (int j = i - 1; j >= 0; j--) {
        dp[i] = dp[j] && wordSet.contains(s.substring(j, i));
        if (dp[i]) {
          break;
        }
      }
    }
    return dp[s.length()];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/545383870/){:target="_blank"}

# 설명
1. 주어진 문자열 s에 문자열의 List인 wordDict의 문자열들이 포함되는지 검증하는 문제이다.

2. 문제를 풀기 위해 변수를 정의한다.
- dp는 문자열 길이보다 하나 크게 정의하여 문자열 포함에 대한 검증에 활용하며, 0번째 값을 true로 초기화한다.
- wordSet은 주어진 문자열의 List를 중복을 제거하여 사용하기 위해 wordDict의 값들을 넣어 초기화 한다.

3. 문자열을 차례대로 반복하여 wordSet에 포함된 단어가 있는지 검증한다.
- dp[i]에 dp[j]의 결과와 wordSet에 문자열 s의 j번째부터 i번째까지 자른 값이 존재하는지 결과를 AND(논리곱) 결과를 넣어준다.
- 만일 dp[i]가 true인 경우 i를 증가시켜 다음 문자열부터 다시 검증한다.

4. 반복이 완료되면 문자열이 포함되는지 검증한 결과인 dp[s.length()]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WordBreak.java){:target="_blank"}에서 확인 가능합니다.