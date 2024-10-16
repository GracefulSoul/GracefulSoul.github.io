---
title: "Leetcode Java Longest Common Prefix"
excerpt: "Leetcode Longest Common Prefix Java 풀이"
last_modified_at: 2021-04-24T17:00:00
header:
  image: /assets/images/leetcode/longest-common-prefix.png
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
[Link](https://leetcode.com/problems/longest-common-prefix/){:target="_blank"}

# 코드
```java
class Solution {

  public String longestCommonPrefix(String[] strs) {
    String prefix = strs[0];
    if (strs.length == 1) {
      return prefix;
    }
    for (int idx = 1; idx < strs.length; idx++) {
      while (strs[idx].indexOf(prefix) != 0) {
        prefix = prefix.substring(0, prefix.length() - 1);
      }
    }
    return prefix;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/483836409/){:target="_blank"}

# 설명
1. 첫 문자열을 주어진 문제의 결과를 저장할 prefix 변수로 저장한다.

2. 문제를 확인해보면 주어진 배열 strs의 크기는 1 ~ 200까지 이므로, 크기가 1인 경우 변수 prefix를 문제의 결과로 반환한다.

3. 주어진 배열 strs의 크기가 2 이상인 경우 반복문을 통해서 각 단어의 공통된 시작 문자열을 탐색한다.
- indexOf 메서드는 해당 문자열이 대상의 문자열에 존재하지 않으면 -1, 존재하면 해당 위치 시작점의 index를 반환되므로 반복문은 0이 아닐 때까지 진행한다.
- 위의 경우를 확인하여 첫 문자열 기준으로 한 문자씩 제거하면서 다른 문자열과 공통된 문자열을 탐색한다.

4. 반복이 끝나면 공통된 문자열을 저장한 prefix 변수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestCommonPrefix.java){:target="_blank"}에서 확인 가능합니다.