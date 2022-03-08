---
title: "Leetcode Java Longest Palindrome"
excerpt: "Leetcode Longest Palindrome Java 풀이"
last_modified_at: 2022-03-08T12:00:00
header:
  image: /assets/images/leetcode/longest-palindrome.png
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
[Link](https://leetcode.com/problems/longest-palindrome/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestPalindrome(String s) {
    int[] count = new int[58];
    for (char c : s.toCharArray()) {
      count[c - 'A']++;
    }
    int length = 0;
    boolean isOdd = false;
    for (int idx = 0; idx < 58; idx++) {
      length += count[idx];
      if (count[idx] % 2 == 1) {
        length--;
        isOdd = true;
      }
    }
    return length + (isOdd ? 1 : 0);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/655534901/){:target="_blank"}

# 설명
1. 주어진 문자열 s를 이용하여 만들 수 있는 가장 긴 회문을 만드는 문제이다.
- 단, 대소문자를 구분하므로 "Aa"는 회문이 되지 않는다.

2. count를 대문자 A부터 소문자 z까지 ASCII 코드의 길이인 58 크기로 초기화 하고, s의 각 문자의 발생 갯수를 count에 넣어준다.

3. 가장 킨 회문의 길이를 저장할 length를 0으로, 해당 회문의 길이가 홀수인지 저장할 isOdd를 false로 초기화한다.

4. 0부터 58까지 idx를 증가시키며 가장 긴 회문의 길이를 저장한다.
- length에 count의 idx번째 값을 더해준다.
- count의 idx번째 값이 홀수인 경우, length를 감소시키고 isOdd를 true로 변경한다.
  - 회문의 길이가 짝수인 경우, 모든 문자의 발생 횟수는 짝수로 존재하여야 한다.

5. 반복이 완료되면 isOdd가 true로 홀수인 경우 length에 1을 더해서, 짝수인 경우 length를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestPalindrome.java){:target="_blank"}에서 확인 가능합니다.