---
title: "Leetcode Java Score of Parentheses"
excerpt: "Leetcode Score of Parentheses Java"
last_modified_at: 2023-03-01T12:40:00
header:
  image: /assets/images/leetcode/score-of-parentheses.png
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
[Link](https://leetcode.com/problems/score-of-parentheses){:target="_blank"}

# 코드
```java
class Solution {

  public int scoreOfParentheses(String s) {
    Stack<Integer> stack = new Stack<>();
    int result = 0;
    for (int i = 0; i < s.length(); i++) {
      if (s.charAt(i) == '(') {
        stack.push(result);
        result = 0;
      } else {
        result = stack.pop() + Math.max(2 * result, 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/score-of-parentheses/submissions/906865525/){:target="_blank"}

# 설명
1. 소괄호를 이용한 아래의 규칙대로 계산된 점수를 반환하는 문제이다.
- "()" 1점이며, "AB"는 A + B의 점수를 가지며 A와 B는 균형잡힌 괄호 문자열이다.
- "(A)"는 $2 \times A$의 점수를 가지며 A는 균형잡힌 괄호 문자열이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- stack은 점수를 계산하기 위한 변수로, stack으로 초기화한다.
- result는 점수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 s의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- s의 i번쨰 문자가 괄호의 시작인 '(' 문자인 경우, stack에 result를 넣어주고, result를 0으로 초기화한다.
- 위의 경우가 아니라면 result에 stack에서 점수를 꺼내서 $2 \times result$와 1 중 큰 값과 더한 결과를 넣어준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ScoreOfParentheses.java){:target="_blank"}에서 확인 가능합니다.