---
title: "Leetcode Java Construct K Palindrome Strings"
excerpt: "Leetcode - 'Construct K Palindrome Strings' 문제 Java 풀이"
last_modified_at: 2025-01-11T11:40:00
header:
  image: /assets/images/leetcode/construct-k-palindrome-strings.png
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
[Link](https://leetcode.com/problems/construct-k-palindrome-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canConstruct(String s, int k) {
    if (s.length() > k) {
      int odd = 0;
      for (char c : s.toCharArray()) {
        odd ^= 1 << (c - 'a');
      }
      return Integer.bitCount(odd) <= k;
    } else {
      return s.length() == k;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/construct-k-palindrome-strings/submissions/1504618593/){:target="_blank"}

# 설명
1. 문자열 s를 k개의 회문 문자열로 분리 가능한지 여부를 검증하는 문제이다.

2. s의 길이가 k 초과인 경우, 아래를 수행한다.
- odd는 홀수 갯수를 저장할 변수로, s의 문자들을 순서대로 c에 넣고 odd에 각 문자의 영문자 순서만큼 1을 좌측으로 이동신 값을 자기 자신의 값과 XOR('^') 비트연산을 수행한 결과로 넣어준다.
- 계산된 odd의 1 비트 갯수가 k 이하인 홀수번 존재하는 문자의 갯수가 k 이하인지 여부를 주어진 문제의 결과로 반환한다.
  - k개 이하의 회문을 만들어야 하므로, 홀수번 반복되는 문자는 k개까지 문자열의 중앙에 넣을 수 있다.

3. s의 길이가 k와 동일한 문자 하나 씩 분리가 가능한 경우만 true, k 초과인 분리해도 만들 수 없는 경우 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConstructKPalindromeStrings.java){:target="_blank"}에서 확인 가능합니다.