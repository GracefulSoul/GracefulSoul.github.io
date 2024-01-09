---
title: "Leetcode Java Remove Outermost Parentheses"
excerpt: "Leetcode Remove Outermost Parentheses Java"
last_modified_at: 2024-01-09T11:30:00
header:
  image: /assets/images/leetcode/remove-outermost-parentheses.png
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
[Link](https://leetcode.com/problems/remove-outermost-parentheses){:target="_blank"}

# 코드
```java
class Solution {

  public String removeOuterParentheses(String s) {
    StringBuilder sb = new StringBuilder();
    int count = 0;
    for (char c : s.toCharArray()) {
      if ((c == '(' && count++ > 0) || (c == ')' && count-- > 1)) {
        sb.append(c);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/remove-outermost-parentheses/submissions/1141005790/){:target="_blank"}

# 설명
1. 문자열 s의 각 괄호마다 외부에 존재하는 괄호를 제거하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 동적 문자열을 생성하기 위한 변수로, StringBuilder로 초기화한다.
- count는 괄호의 갯수를 계산하기 위한 변수로, 0으로 초기화한다.

3. 문자열 s의 각 문자를 c에 순차적으로 넣어 괄호의 시작 전과 후의 문자를 제외하고 sb에 문자를 이어준다.

4. 반복이 완료되면 완성된 문자열이 저장된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveOutermostParentheses.java){:target="_blank"}에서 확인 가능합니다.