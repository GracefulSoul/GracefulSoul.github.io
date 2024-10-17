---
title: "Leetcode Java Maximum Nesting Depth of the Parentheses"
excerpt: "Leetcode Easy - 'Maximum Nesting Depth of the Parentheses' 문제 Java 풀이"
last_modified_at: 2024-04-04T18:20:00
header:
  image: /assets/images/leetcode/maximum-nesting-depth-of-the-parentheses.png
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
[Link](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxDepth(String s) {
    int count = 0;
    int result = 0;
    for (char c : s.toCharArray()) {
      switch (c) {
        case '(': result = Math.max(result, ++count); break;
        case ')': count--; break;
        default:
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/submissions/1222934960/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 유효한 괄호 문자열의 최대 깊이를 반환하는 문제이다.
- 유효한 괄호 문자열(이하 VPS)는 아래의 규칙을 따른다.
  - 빈 문자열은 "", 단일 문자는 "(", ")"를 제외한 문자이다.
  - VPS를 만족하는 A와 B는 AB로 표기한다.
  - VPS를 만족하는 A는 (A)로 표기한다.
- VPS의 최대 깊이는 아래의 규칙을 따른다.
  - ""의 깊이는 0이다.
  - "(", ")"를 제외한 단일 문자의 깊이는 0이다.
  - $A + B$의 깊이는 A와 B의 깊이 중 가장 큰 깊이를 나타낸다.
  - "(A)"의 깊이는 $1 + A 문자열의 깊이$이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 괄호의 수를 저장할 변수로, 0으로 초기화한다.
- result는 최대 깊이를 저장할 변수로, 0으로 초기화한다.

3. s의 각 문자들을 c에 순차적으로 넣고 아래를 수행한다.
- c가 '(' 문자인 경우, result에 result와 count를 증가시킨 다음 문자의 VPS 깊이 중 큰 값을 넣어준다.
- c가 ')' 문자인 경우, count를 감소시켜 VPS의 깊이를 감소시킨다.

4. 반복이 완료되면 최대 깊이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumNestingDepthOfTheParentheses.java){:target="_blank"}에서 확인 가능합니다.