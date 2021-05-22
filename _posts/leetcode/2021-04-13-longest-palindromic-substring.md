---
title: "Leetcode Java Longest Palindromic Substring"
excerpt: "Leetcode Longest Palindromic Substring Java 풀이"
last_modified_at: 2021-04-13T20:00:00
header:
  image: /assets/images/leetcode/longest-palindromic-substring.png
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
[Link](https://leetcode.com/problems/longest-palindromic-substring/){:target="_blank"}

# 코드
```java
class Solution {

  public String longestPalindrome(String s) {
    int start = 0;
    int end = 0;
    for (int i = 0; i < s.length(); i++) {
      int len = Math.max(expandAroundCenter(s, i, i), expandAroundCenter(s, i, i + 1));
      if (len > end - start) {
        start = i - (len - 1) / 2;
        end = i + len / 2;
      }
    }
    return s.substring(start, end + 1);
  }

  private int expandAroundCenter(String s, int left, int right) {
    while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
      left--;
      right++;
    }
    return right - left - 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/480056605/){:target="_blank"}

# 설명
1. 주어진 문자열 s에서 가장 긴 반복 문자열을 추출하기 위해서 변수 start와 end를 정의한다.

2. 주어진 문자열 s의 길이만큼 반복문을 통해 가장 긴 반복 문자열의 시작과 끝 index를 탐색한다.
- 반복은 좌측 index가 0보다 크거나 같고, 우측 index가 주어진 문자열 s의 길이보다 작은 값까지 반복한다.
- 주어진 문자열의 i번째 index부터 좌측과 우측의 값이 같은지를 차례대로 비교한다.
- 주어진 문자열의 i번째 index와 i + 1번째 index의 값이 같으면, 좌측과 우측의 값이 같은지를 차례대로 비교한다.
- 위의 두 경우 중 큰 값을 길이로 결정한다.

3. 만일 2번의 결과로 나온 길이가 end - start보다 크다면 start와 end 값을 수정한다.
- 변수 start는 index i 기준으로 $\frac{(len - 1)}{2}$를 뺀 값으로 설정한다.
- 변수 end는 index i 기준으로 $\frac{len}{2}$를 더한 값으로 설정한다.

4. 반복이 끝나면 주어진 문자열 s에서 변수 start번째 문자부터 변수 end까지 문자까지 잘라서 주어진 문제의 결과로 제출한다.
- end까지 자르는데 substring(start, end + 1)인 이유는 substring 메서드가 start번째 부터 end + 1번째 전까지 자르기 때문이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestPalindromicSubstring.java){:target="_blank"}에서 확인 가능합니다.