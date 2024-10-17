---
title: "Leetcode Java Evaluate Reverse Polish Notation"
excerpt: "Leetcode - 'Evaluate Reverse Polish Notation' 문제 Java 풀이"
last_modified_at: 2021-09-07T13:00:00
header:
  image: /assets/images/leetcode/evaluate-reverse-polish-notation.png
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
[Link](https://leetcode.com/problems/evaluate-reverse-polish-notation/){:target="_blank"}

# 코드
```java
class Solution {

  public int evalRPN(String[] tokens) {
    Stack<Integer> stack = new Stack<>();
    for (String token : tokens) {
      switch (token) {
        case "+":
          stack.push(stack.pop() + stack.pop());
          break;
        case "-":
          stack.push((-1) * stack.pop() + stack.pop());
          break;
        case "*":
          stack.push(stack.pop() * stack.pop());
          break;
        case "/":
          int n1 = stack.pop(), n2 = stack.pop();
          stack.push(n2 / n1);
          break;
        default:
          stack.push(Integer.parseInt(token));
      }
    }
    return stack.pop();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/550807774/){:target="_blank"}

# 설명
1. 주어진 문자열 배열 tokens를 이용하여 주어진 숫자와 연산 기호를 이용하여 최종 연산된 값을 구하는 문제이다.
- 값의 패턴은 숫자1, 숫자2, 연산자1 순으로 들어가서 숫자1 연산자1 숫자2 형식으로 구하면 된다.
- Ex) ["1", "2", "+"] -> $1 + 2 = 3$, ["1", "2", "3", "-", "+"] -> $1 + (2 - 3) = 0$

2. 문자열을 순차적으로 넣고 [FILO](https://en.wikipedia.org/wiki/FIFO_and_LIFO_accounting#LIFO){:target="_blank"}로 추출하기 위해 변수 stack을 정의한다.

3. 주어진 문자열의 배열 tokens를 반복하여 숫자들의 연산을 수행한다.
- "+", "-", "*", "/" 연산자가 나올 경우, stack에 넣은 최근 두 값을 가져와 해당 연산을 수행하여 stack에 다시 넣어준다.
- 그 외의 문자열은 Integer 형태로 형 변환을 수행하여 stack에 넣어준다.

4. 반복이 완료되면 stack에 저장된 최종 연산된 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EvaluateReversePolishNotation.java){:target="_blank"}에서 확인 가능합니다.