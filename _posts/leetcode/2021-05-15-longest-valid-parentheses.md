---
title: "Leetcode Java Longest Valid Parentheses"
excerpt: "Leetcode Longest Valid Parentheses Java 풀이"
last_modified_at: 2021-05-15T09:00:00
header:
  image: /assets/images/leetcode/longest-valid-parentheses.png
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
[Link](https://leetcode.com/problems/longest-valid-parentheses/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestValidParentheses(String s) {
    Stack<Integer> stack = new Stack<>();
    int result = 0;
    for (int idx = 0; idx < s.length(); idx++) {
      if (s.charAt(idx) == ')' && !stack.isEmpty() && s.charAt(stack.peek()) == '(') {
        stack.pop();
        result = Math.max(result, stack.isEmpty() ? idx + 1 : idx - stack.peek());
      } else {
        stack.push(idx);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/493237946/){:target="_blank"}

# 설명
1. 주어진 소괄호로 이루어진 문자열 s를 검증하기 위한 Stack과 문제의 결과를 저장할 result 변수를 선언한다.

2. 주어진 문자열 s의 길이만큼 반복하면서 문자열 검증을 수행한다.
  - 주어진 문자열 s의 idx번째 문자가 '('일 경우, 해당 index를 Stack에 저장한다.
  - 주어진 문자열 s의 idx번째 문자가 ')'일 경우, Stack이 비어있지 않고, 주어진 문자열 s의 Stack에 최근 저장된 인덱스의 문자가 '('인 경우 문자열의 길이를 저장한다.
    - Stack에 최근 저장된 인덱스의 문자 검증이 끝났으므로, 해당 값은 pop()으로 제거해준다.
    - 주어진 문제의 결과를 저장한 result 변수와 Stack이 비어있으면 idx + 1, 그렇지 않으면 idx - stack에 남은 최근 인덱스의 결과 중 큰 값을 result 변수에 주입한다.
      - Stack이 비어있다는 것은, 모든 값이 소괄호의 조합으로 끝난 경우이므로, 해당 위치의 인 idx에 + 1을 더하여 길이를 산정한다.
      - Stack이 비어있지 않다는 것은, '(' 문자열이 남아있는 경우이므로, 해당 인덱스를 idx에서 빼서 문자열 중간의 소괄호의 조합의 길이를 산정한다.

3. 반복이 종료되면 문제의 결과를 저장한 reulst 변수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestValidParentheses.java){:target="_blank"}에서 확인 가능합니다.