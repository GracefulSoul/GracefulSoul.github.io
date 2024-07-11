---
title: "Leetcode Java Reverse Substrings Between Each Pair of Parentheses"
excerpt: "Leetcode Reverse Substrings Between Each Pair of Parentheses Java"
last_modified_at: 2024-07-11T18:00:00
header:
  image: /assets/images/leetcode/reverse-substrings-between-each-pair-of-parentheses.png
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
[Link](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/){:target="_blank"}

# 코드
```java
class Solution {

  private int index;

  public String reverseParentheses(String s) {
    this.index = 0;
    return this.reverseParentheses(s.toCharArray());
  }

  private String reverseParentheses(char[] charArray) {
    StringBuilder sb = new StringBuilder();
    while (this.index < charArray.length) {
      switch (charArray[this.index]) {
        case ')': this.index++; return sb.reverse().toString();
        case '(': this.index++; sb.append(this.reverseParentheses(charArray)); break;
        default: sb.append(charArray[this.index++]); break;
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/submissions/1317414744/){:target="_blank"}

# 설명
1. 문자열 s를 괄호 안 문자열을 순서대로 거꾸로 문자열을 만들어 괄호가 제거된 상태로 반환하는 문제이다.

2. 전역 변수인 index는 문자열 s의 위치를 저장할 변수이다.

3. index를 0으로 초기화하고 4번에서 정의한 reverseParentheses(char[] charArray) 메서드에 s를 문자 배열로 변환하여 수행한 결과를 반환한다.

4. 재귀 호출을 통해 문자열을 생성할 reverseParentheses(char[] charArray) 메서드를 정의한다.
- sb는 동적으로 문자열 생성하기 위한 변수로, StringBuilder로 초기화한다.
- index가 charArray의 길이 미만까지 아래를 바놉ㄱ한다.
  - charArray[index]가 ')' 문자이면 문자열의 끝이므로, index를 증가시키고 sb를 거꾸로 반전시킨 문자열로 변환하여 반환한다.
  - charArray[index]가 '(' 문자이면 문자열의 시작이므로, index를 증가시키고 sb에 재귀 호출한 결과를 넣어준다.
  - 그 외의 문자인 경우, sb에 charArray[index]의 문자를 넣고 index를 증가시켜준다.
- 반복이 완료되면 sb를 문자열로 변환하여 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseSubstringsBetweenEachPairOfParentheses.java){:target="_blank"}에서 확인 가능합니다.