---
title: "Leetcode Java Parsing A Boolean Expression"
excerpt: "Leetcode Hard - 'Parsing A Boolean Expression' 문제 Java 풀이"
last_modified_at: 2024-05-13T19:20:00
header:
  image: /assets/images/leetcode/parsing-a-boolean-expression.png
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
[Link](https://leetcode.com/problems/parsing-a-boolean-expression/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean parseBoolExpr(String expression) {
    Stack<Character> stack = new Stack<>();
    for (char c : expression.toCharArray()) {
      if (c == ')') {
        Set<Character> seen = new HashSet<>();
        while (stack.peek() != '(') {
          seen.add(stack.pop());
        }
        stack.pop();
        switch (stack.pop()) {
          case '&': stack.push(seen.contains('f') ? 'f' : 't'); break;
          case '|': stack.push(seen.contains('t') ? 't' : 'f'); break;
          default: stack.push(seen.contains('t') ? 'f' : 't'); break;
        }
      } else if (c != ',') {
        stack.push(c);
      }
    }
    return stack.pop() == 't';
  }

}
```

# 결과
[Link](https://leetcode.com/problems/parsing-a-boolean-expression/submissions/1256814527/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 부울 표현법인 expression이 유효한지를 검증하는 문제이다.
- 't'는 true, 'f'는 false를 의미한다.
- '!(subExpr)'는 부분 표현법인 subExpr의 논리적 NOT 연산을 의미한다.
- '&(subExpr<sub>1</sub>, subExpr<sub>2</sub>, ..., subExpr<sub>n</sub>)'은 각 부분 표현법인 subExpr<sub>1</sub>, subExpr<sub>2</sub>, ..., subExpr<sub>n</sub>의 논리적 AND 연산을 의미한다.
- '|(subExpr<sub>1</sub>, subExpr<sub>2</sub>, ..., subExpr<sub>n</sub>)'은 각 부분 표현법인 subExpr<sub>1</sub>, subExpr<sub>2</sub>, ..., subExpr<sub>n</sub>의 논리적 OR 연산을 의미한다.

2. stack은 각 표현식의 값을 순차적으로 넣었다 빼기 위한 변수로, Stack으로 초기화한다.

3. expression의 각 문자를 순차적으로 c에 넣어 아래를 수행한다.
- c가 ')' 문자인 경우, 아래를 수행한다.
  - seen은 탐색한 문자들을 저장할 변수로, 중복을 제거하기 위해 HashSet으로 초기화하고 stack 내 다음 문자가 '(' 문자가 아닐 때 까지 seen에 stack의 값을 꺼내 넣어준다.
  - stack의 다음 문자인 '(' 문자를 꺼내 제거해준다.
  - stack의 다음 문자가 '&'이면 stack에 seen 내 'f' 문자가 존재할 경우 논리적 AND 연산의 결과는 false이므로, 'f'를 아니면 't'를 넣어준다.
  - stack의 다음 문자가 위의 경우가 아니라 '|'이면 stack에 seen 내 't' 문자가 존재할 경우 논리적 OR 연산의 결과는 true이므로, 't'를 아니면 'f'를 넣어준다.
  - stack의 다음 문자가 위의 두 경우가 아니라면 stack에 seen 내 't' 문자가 존재할 경우 반대의 값으로, 'f'를 아니면 't'를 넣어준다.
- c가 위의 경우가 아니면서 ',' 문자가 아닌 경우, stack에 c를 넣어준다.

4. stack 내 값을 꺼낸 문자가 't'인지를 검증한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ParsingABooleanExpression.java){:target="_blank"}에서 확인 가능합니다.