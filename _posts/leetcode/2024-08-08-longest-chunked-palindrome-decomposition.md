---
title: "Leetcode Java Longest Chunked Palindrome Decomposition"
excerpt: "Leetcode Hard - 'Longest Chunked Palindrome Decomposition' 문제 Java 풀이"
last_modified_at: 2024-08-08T19:20:00
header:
  image: /assets/images/leetcode/longest-chunked-palindrome-decomposition.png
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
[Link](https://leetcode.com/problems/longest-chunked-palindrome-decomposition/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestDecomposition(String text) {
    int length = text.length();
    for (int i = 0; i < length / 2; i++) {
      if (text.substring(0, i + 1).equals(text.substring(length - 1 - i, length))) {
        return 2 + this.longestDecomposition(text.substring(i + 1, length - 1 - i));
      }
    }
    return length == 0 ? 0 : 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-chunked-palindrome-decomposition/submissions/1348732394/){:target="_blank"}

# 설명
1. text가 주어지면 비어있지 않은 k개의 부분 문자열로 아래를 만족하는 최대 k를 구하는 문제이다.
- text는 각 부분 문자열의 조합으로 완성할 수 있다.
- 1 <= i <= k를 만족할 때, i번째 부분 문자열은 $k - i + 1$번째 부분 문자열과 동일하다.

2. length에 text의 길이를 넣어준 후, 0부터 $\frac{length}{2}$까지 i를 증가시키면서 아래를 반복한다.
- text의 처음 위치부터 $i + 1$ 위치 미만까지 문자열과 $length - 1 - i$ 위치부터 마지막 위치까지 문자열이 동일한 두 번째 조건을 만족하는 경우, 아래의 두 값의 합을 반환한다.
  - 두 번째 조건을 만족하는 부분 문자열의 갯수인 2.
  - 두 문자열 사이의 문자열을 재귀 호출한 결과.

3. 반복이 완료되면 length가 0인 text가 빈 문자열이면 0을, 아니면 하나의 부분 문자열이므로 1을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestChunkedPalindromeDecomposition.java){:target="_blank"}에서 확인 가능합니다.