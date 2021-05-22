---
title: "Leetcode Java Implement strStr() Array"
excerpt: "Leetcode Implement strStr() Java 풀이"
last_modified_at: 2021-05-10T21:10:00
header:
  image: /assets/images/leetcode/implement-strstr.png
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
[Link](https://leetcode.com/problems/implement-strstr/){:target="_blank"}

# 코드
```java
class Solution {

  public int strStr(String haystack, String needle) {
    if (needle.length() == 0) {
      return 0;
    }
    if (haystack.length() == 0) {
      return -1;
    }
    for (int i = 0; i < haystack.length(); i++) {
      if (i + needle.length() > haystack.length()) {
        return -1;
      }
      for (int j = 0; j < needle.length(); j++) {
        if (haystack.charAt(i + j) != needle.charAt(j)) {
          break;
        } else if (j == needle.length() - 1) {
          return i;
        }
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/491571524/){:target="_blank"}

# 설명
1. 주어진 문제는 Java에서 String 내 indexOf 메서드를 보면 금방 파악하는 문제이다.

2. 주어진 변수 needle의 길이가 0인 경우, 소속된 문자열이 어느 위치든 포함이 되므로 0을 주어진 문제의 결과로 반환한다.
- needle의 길이가 0인 경우는 ""이므로, 어느 문자열이든 첫 문자열에 포함된다.

3. 주어진 변수 haystack의 길이가 0인 경우, 주어진 변수 needle이 어떠한 값이더라도 포함되지 않으므로 -1을 주어진 문제의 결과로 반환한다.

4. haystack과 needle을 각 문자 별로 반복하여 결과를 탐색한다.
- 단 haystack의 시작 문자의 index + needle의 문자열 길이가 haystack의 문자열 길이보다 클 경우에는 포함된 단어가 없으므로, -1을 주어진 문제의 결과로 반환한다.
- 만일 haystack의 i번째 문자와 needle의 0번째 문자열이 같은 경우 j를 증가시키며 비교를 한다.
- 만일 j의 길이가 needle의 길이와 같다면, needle의 문자열과 일치한 haystack의 첫 index인 i를 주어진 문제의 결과로 반환한다.

5. 반복이 종료되면, 일치된 결과가 존재하지 않으므로 -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ImplementStrStr.java){:target="_blank"}에서 확인 가능합니다.