---
title: "Leetcode Java Minimum Add to Make Parentheses Valid"
excerpt: "Leetcode Minimum Add to Make Parentheses Valid Java"
last_modified_at: 2023-05-08T19:25:00
header:
  image: /assets/images/leetcode/minimum-add-to-make-parentheses-valid.png
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
[Link](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid){:target="_blank"}

# 코드
```java
class Solution {

  public int minAddToMakeValid(String s) {
    int left = 0;
    int right = 0;
    for (int i = 0; i < s.length(); i++) {
      if (s.charAt(i) == '(') {
        right++;
      } else if (right > 0) {
        right--;
      } else {
        left++;
      }
    }
    return left + right;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/submissions/947191488/){:target="_blank"}

# 설명
1. 문자열 s가 유효한 문자열이 되기 위해서 모든 위치에 괄호의 시작 문자인 '('와 종료 문자인 ')'를 삽입하여 유효한 문자열이 되기 위한 최소 횟수를 구하는 문제이다.
- 유효한 문자열이 되기 위해서는 괄호의 시작 문자인 '('와 종료 문자인 ')'의 짝이 맞거나 존재하지 않아야 한다.

2. left와 right는 괄호의 시작 문자인 '('와 종료 문자인 ')'의 갯수를 계산할 변수로, 둘 다 0으로 초기화한다.

3. 0부터 s의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- s의 i번째 문자가 '('인 경우, 우측에 ')' 문자가 필요하므로 right를 증가시킨다.
- 위의 경우가 아니면서 right가 0 초과인 경우, ')'문자로 이어지므로 right를 감소시킨다.
- 위 모든 경우가 아니라면 '(' 문자를 현재의 ')' 문자 이전에 넣어야 하므로, left를 증가시킨다.

4. 반복이 완료되면 추가한 괄호 문자의 수인 $left + right$를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumAddToMakeParenthesesValid.java){:target="_blank"}에서 확인 가능합니다.