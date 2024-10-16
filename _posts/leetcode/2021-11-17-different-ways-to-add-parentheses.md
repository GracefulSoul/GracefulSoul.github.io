---
title: "Leetcode Java Different Ways to Add Parentheses"
excerpt: "Leetcode Different Ways to Add Parentheses Java 풀이"
last_modified_at: 2021-11-17T12:00:00
header:
  image: /assets/images/leetcode/different-ways-to-add-parentheses.png
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
[Link](https://leetcode.com/problems/different-ways-to-add-parentheses/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> diffWaysToCompute(String expression) {
    List<Integer> result = new ArrayList<>();
    for (int idx = 0; idx < expression.length(); idx++) {
      char c = expression.charAt(idx);
      if (c == '-' || c == '+' || c == '*') {
        List<Integer> first = this.diffWaysToCompute(expression.substring(0, idx));
        List<Integer> second = this.diffWaysToCompute(expression.substring(idx + 1));
        for (int num1 : first) {
          for (int num2 : second) {
            switch (c) {
              case '-':
                result.add(num1 - num2);
                break;
              case '+':
                result.add(num1 + num2);
                break;
              case '*':
                result.add(num1 * num2);
                break;
            }
          }
        }
      }
    }
    if (result.isEmpty()) {
      result.add(Integer.valueOf(expression));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/588415909/){:target="_blank"}

# 설명
1. 수학 계산식이 저장된 주어진 문자열 expression를 기반으로 부분 계산을 활용하여 나올 수 있는 값들을 구하는 문제이다.
- 부분 계산이란 소괄호()를 특정 연산 단위로 분리해서 계산을 한 결과를 말한다.

2. 부분 계산의 결과를 저장할 컬렉션인 result를 컬렉션으로 정의한다.

3. expression을 한 글자 씩 반복하여 idx번째 문자가 '-', '+', '*'의 계산 연산자인 경우, 아래를 수행한다.
- first에 expression의 처음부터 idx번째 전까지 각 부분 계산을 결과를 넣기 위해 재귀 호출을 수행하고 해당 결과를 넣어준다.
- seconde에 expression의 $idx + 1$번째부터 끝까지 각 부분 계산을 결과를 넣기 위해 재귀 호출을 수행하고 해당 결과를 넣어준다.

4. first와 second를 모두 반복하여 c의 연산자에 따른 결과를 result에 넣어준다.

5. 반복이 완료되고 result가 비어있으면 재귀 호출을 통해서 expression에 숫자만 넘어온 경우이므로, result에 expression을 형 변환하여 넣어준다.

6. expression을 이용한 결과를 모두 저장한 result를 반환하며, 최초 호출의 경우 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DifferentWaysToAddParentheses.java){:target="_blank"}에서 확인 가능합니다.