---
title: "Leetcode Java Valid Parentheses"
excerpt: "Leetcode Valid Parentheses Java 풀이"
last_modified_at: 2021-04-30T22:00:00
header:
  image: /assets/images/leetcode/valid-parentheses.png
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
[Link](https://leetcode.com/problems/valid-parentheses/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();
    for (char c : s.toCharArray()) {
      switch (c) {
      case '(':
      case '{':
      case '[':
        stack.push(c);
        break;
      case ')':
        if (stack.isEmpty() || !stack.pop().equals('(')) {
          return false;
        }
        break;
      case '}':
        if (stack.isEmpty() || !stack.pop().equals('{')) {
          return false;
        }
        break;
      case ']':
        if (stack.isEmpty() || !stack.pop().equals('[')) {
          return false;
        }
        break;
      }
    }
    return stack.isEmpty();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/487044545/){:target="_blank"}

# 설명
1. 주어진 문제의 검증을 위해 후입선출의 [Stack](https://docs.oracle.com/javase/8/docs/api/java/util/Stack.html)을 사용하여 변수 stack을 정의한다.
- 문제의 요점은 소, 중, 대 괄호가 열고 닫힘이 정확히 맞는 부분을 요구하는 것이므로, 이 부분에 초점을 맞추어 Stack을 사용한다.
- 마지막으로 '(' 문자가 들어왔을 경우, ')'문자가 다음에 나오면 괄호의 순서에 맞게 닫히는 경우이다.
- 마지막으로 '(' 문자가 들어왔을 경우, '{', '[' 문자가 나오면 그대로 누적하여 반대 문자가 나와서 괄호가 정상적으로 닫히는지 여부를 확인하여야 한다.

2. 1번의 검증이 끝나서 변수 stack은 비어있을 것이므로, stack에 남은 문자가 남아있는지 여부를 주어진 문제의 결과로 제공한다.
- 순차적으로 열고 닫은 괄호의 경우, stack에는 아무 값도 없을 것이다.
- 만일 순차적이지 않은 문자열의 경우, stack에는 값이 남아있어야한다. (Ex. 문자열 '({))'의 경우, '}' 문자가 나오지 않았으므로 반복은 종료되고 '{'가 남아있는 stack은 비어있지 않으므로 주어진 문제의 결과는 false가 반환될 것이다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidParentheses.java){:target="_blank"}에서 확인 가능합니다.