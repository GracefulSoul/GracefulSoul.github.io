---
title: "Leetcode Java Valid Parenthesis String"
excerpt: "Leetcode - 'Valid Parenthesis String' 문제 Java 풀이"
last_modified_at: 2022-10-01T10:10:00
header:
  image: /assets/images/leetcode/valid-parenthesis-string.png
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
[Link](https://leetcode.com/problems/valid-parenthesis-string){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkValidString(String s) {
    int min = 0;
    int max = 0;
    for (char c : s.toCharArray()) {
      switch (c) {
        case '(':
          max++;
          min++;
          break;
        case ')':
          max--;
          min--;
          break;
        case '*':
          max++;
          min--;
          break;
      }
      if (max < 0) {
        return false;
      }
      min = Math.max(min, 0);
    }
    return min == 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/812372966/){:target="_blank"}

# 설명
1. s는 '(', ')', '*' 문자들만 포함된 문자열로, 아래의 조건을 만족하는지 검증하는 문제이다.
- 왼쪽에 '(' 문자가 존재하는 경우, 오른쪽에 ')' 문자가 존재하여 쌍을 반드시 이루어야 한다.
- '(' 문자는 ')' 문자 앞에 와야 한다.
- '*' 문자는 '(' 문자 혹은 ')' 문자, 빈 문자인 '' 문자로 취급이 가능하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- min은 규칙을 만족하기 위한 '('문자와 ')'문자의 최소 차잇값을 저장할 변수로, 0으로 초기화한다.
- max는 위와 동일하지만 최대 차잇값을 저장할 변수로, 0으로 초기화한다.

3. s의 모든 문자를 c에 넣어 아래를 순서대로 반복한다.
- c가 '(' 문자의 경우 열린 괄호가 생겼으므로, max와 min을 증가시킨다.
- c가 ')' 문자의 경우 딛힌 괄호가 생겼으므로, max와 min을 감소시킨다.
- c가 '*' 문자의 경우 아무 문자의 처리가 가능하므로, max를 증가시키고 min을 감소시킨다.
  - '('인 경우 max는 증가 가능하며, ')'인 경우 min은 감소가 가능하기 떄문이다.
- max가 0보다 작게되면 조건을 충족하는 경우의 수가 없으므로, false를 주어진 문제의 결과로 반환한다.
- max가 0보다 크면서 min이 음수가 되는 경우는 가능한 경우가 존재한다는 의미이므로, min에 min과 0 중 큰 값을 반환한다.

4. 반복이 완료되면 min이 0인지를 검증하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidParenthesisString.java){:target="_blank"}에서 확인 가능합니다.