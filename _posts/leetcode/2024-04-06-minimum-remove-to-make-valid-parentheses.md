---
title: "Leetcode Java Minimum Remove to Make Valid Parentheses"
excerpt: "Leetcode Medium - 'Minimum Remove to Make Valid Parentheses' 문제 Java 풀이"
last_modified_at: 2024-04-06T16:00:00
header:
  image: /assets/images/leetcode/minimum-remove-to-make-valid-parentheses.png
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
[Link](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/){:target="_blank"}

# 코드
```java
class Solution {

  public String minRemoveToMakeValid(String s) {
    char[] charArray = s.toCharArray();
    int open = 0;
    for (int i = 0; i < charArray.length; i++) {
      switch (charArray[i]) {
        case '(': open++; break;
        case ')':
          if (open == 0) {
            charArray[i] = '.';
          } else {
            open--;
          }
          break;
        default: break;
      }
    }
    for (int i = charArray.length - 1; i >= 0; i--) {
      if (open > 0 && charArray[i] == '(') {
        charArray[i] = '.';
        open--;
      }
    }
    StringBuilder sb = new StringBuilder();
    for (char c : charArray) {
      if (c != '.') {
        sb.append(c);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/submissions/1224619191/){:target="_blank"}

# 설명
1. '(', ')', 영소문자로 이루어진 s를 이용하여 아래의 규칙을 만족하는 유효한 문자열을 반환하는 문제이다.
- 결과 문자열의 괄호가 유효하도록 '(', ')'를 최소한 제거할 수 있다.
- 괄호 문자열은 아래의 경우에 유효하다.
  - 빈 문자열 혹은 영소문자로 이루어진 문자열.
  - A와 B 문자열이 이어진 AB 문자열.
  - (A)로 표기된 A가 유효한 문자열.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 문자열 s를 문자 배열로 변환하여 저장한 변수이다.
- open은 '(' 문자의 갯수를 계산할 변수로, 0으로 초기화한다.

3. 0부터 charArray의 길이 미만까지 i를 증가시키며, 문자열 s의 좌측에서 우측으로 아래를 반복하여 괄호를 검증한다.
- charArray[i]의 문자에 따라 아래를 수행한다.
  - '(' 문자의 경우, open을 증가시킨다.
  - ')' 문자의 경우, open이 0인 경우 charArray[i]에 '.' 문자를 넣어 제거해준다.
  - 그 외의 경우, 반복을 계속 수행한다.

4. charArray의 길이보다 1 작은 값부터 0이상일 때 까지 i를 감소시키며, 문자열 s의 우측에서 좌측으로 아래를 반복하여 괄호를 재 검증한다.
- open이 0 초과이면서 charArray[i]의 문자가 '('인 경우, charArray[i]에 '.' 문자를 넣어 제거하고 open을 감소시킨다.

5. charArray에서 '.' 문자를 제거한 문자들을 StringBuilder를 통해 동적으로 문자열로 만들어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumRemoveToMakeValidParentheses.java){:target="_blank"}에서 확인 가능합니다.