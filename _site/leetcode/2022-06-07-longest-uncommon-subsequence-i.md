---
title: "Leetcode Java Longest Uncommon Subsequence I"
excerpt: "Leetcode Longest Uncommon Subsequence I Java"
last_modified_at: 2022-06-07T19:00:00
header:
  image: /assets/images/leetcode/longest-uncommon-subsequence-i.png
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
[Link](https://leetcode.com/problems/longest-uncommon-subsequence-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int findLUSlength(String a, String b) {
    return a.equals(b) ? -1 : Math.max(a.length(), b.length());
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/716416214/){:target="_blank"}

# 설명
1. 영소문자로만 이루어진 문자열 a와 b 중 유일한 가장 긴 [부분 수열](https://en.wikipedia.org/wiki/Subsequence){:target="_blank"} 문자열의 길이를 구하는 문제로, 유일한 부분 수열 문자열이 존재하지 않으면 -1을 반환한다.

2. a와 b의 가장 긴 부분 수열 문자열은 a와 b이므로 아래의 검증을 통해 결과를 반환한다.
- a와 b가 동일한 경우 부분 수열 문자열 모두가 동일하므로, -1을 주어진 문제의 결과로 반환한다.
- a와 b가 동일하지 않은 경우 a와 b 중 가장 긴 문자열의 길이가 두 문자열 중 유일한 가장 긴 부분 수열 문자열의 길이이므로, 해당 값을 주어진 문제의 결과로 반환한다.

# 해설
- 제시된 문제가 헷갈릴 수 있으므로 해설을 추가하면, 단순히 제시하는 <b>Longest Uncommon Subsequence(가장 긴 흔치 않은 부분 수열)</b>에 초점을 잡아야 한다.
  - 문제는 Uncommon(흔치 않은)이라고 제시하지만 내용을 확인해 보면 Unique(유일한)가 맞지 않을까 한다.
- 모든 문자열의 부분 수열 중 가장 긴 값은 자기 자신이다.
  - "abcde"의 부분 수열은 공백인 [""] 부터 한 문자로 이루어진 ["a", ... , "e"] ~ 자기 자신인 ["abcde"] 까지 존재하므로, <b>Longest Subsequence(가장 긴 부분 수열)</b>에 해당하는 문자열은 자기 자신인 "abcde"일 수 밖에 없다.
- 제시된 a와 b 문자열이 동일하면 부분 수열 문자열은 동일할 수 밖에 없으므로, <b>Uncommon Subsequence(흔치않은 부분 수열)</b>은 존재하지 않는다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestUncommonSubsequenceI.java){:target="_blank"}에서 확인 가능합니다.