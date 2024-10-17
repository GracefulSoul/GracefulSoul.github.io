---
title: "Leetcode Java Shortest Palindrome"
excerpt: "Leetcode - 'Shortest Palindrome' 문제 Java 풀이"
last_modified_at: 2021-10-19T09:00:00
header:
  image: /assets/images/leetcode/shortest-palindrome.png
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
[Link](https://leetcode.com/problems/shortest-palindrome/){:target="_blank"}

# 코드
```java
class Solution {

  public String shortestPalindrome(String s) {
    int start = 0;
    for (int end = s.length() - 1; end >= 0; end--) {
      if (s.charAt(start) == s.charAt(end)) {
        start++;
      }
    }
    if (start == s.length()) {
      return s;
    }
    String str = s.substring(start);
    return new StringBuilder(str)
        .reverse()
        .append(this.shortestPalindrome(s.substring(0, start)))
        .append(str)
        .toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/573448815/){:target="_blank"}

# 설명
1. 주어진 문자열 s를 이용하여 최소 크기의 회문(앞뒤로 동일한 문자열)을 만드는 문제이다.

2. 지역 변수 start를 0으로 정의하고, 문자열 s를 마지막 자리부터 첫 자리까지 반복하여 회문이 되는 구간을 찾는다.
- s의 start번째 문자와 s의 end번째 문자가 동일하다면 start를 증가시켜 회문이 되는 문자열의 구간을 확인한다.

3. 반복이 완료되고 start와 주어진 문자열 s의 길이가 동일한 경우, s가 회문이므로 s를 주어진 문제의 결과로 반환한다.

4. 지역 변수 str을 주어진 문자열 s의 start 위치의 문자 부터 마지막 문자까지 잘라 넣어준다.
- 구해진 start 위치의 문자부터 마지막 문자는 회문이 되는 문자열을 제외한 문자로, 접두와 접미에 넣어줄 문자를 임시 보관한다.

5. 새 StringBuilder를 정의하여 str과 재귀 호출을 이용하여 회문을 만들어 주어진 문제의 결과로 반환한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.
- 빈 StringBuilder에 str을 넣고, 문자열의 앞뒤를 반전시켜준다.
  - 회문을 만들기 위해 회문이 되는 구간을 제외한 나머지 문자열을 앞뒤로 넣어주기 위해서, 처음 들어가는 접두 부분은 반전시켜 넣어준다.
- 주어진 문자열 s의 첫 문자부터 start 위치의 문자까지 문자열을 이용하여 재귀 호출을 수행하고, 해당 결과를 위의 문자열에 이어준다.
  - 재귀 호출을 통해 회문이 되는 문자열을 검증하여 문자열을 이어주기 위함이다.
- 마지막으로 다시 str을 넣고, 문자열로 변경하여 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestPalindrome.java){:target="_blank"}에서 확인 가능합니다.