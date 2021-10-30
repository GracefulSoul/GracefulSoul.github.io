---
title: "Leetcode Java Basic Calculator"
excerpt: "Leetcode Basic Calculator Java 풀이"
last_modified_at: 2021-10-30T13:00:00
header:
  image: /assets/images/leetcode/basic-calculator.png
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
[Link](https://leetcode.com/problems/basic-calculator/){:target="_blank"}

# 코드
```java
class Solution {

  public int calculate(String s) {
    int result = 0;
    int length = s.length();
    int sign = 1;
    Stack<Integer> stack = new Stack<>();
    for (int idx = 0; idx < length; idx++) {
      char c = s.charAt(idx);
      switch (c) {
        case ' ':
          break;
        case '+':
          sign = 1;
          break;
        case '-':
          sign = -1;
          break;
        case '(':
          stack.push(result);
          stack.push(sign);
          result = 0;
          sign = 1;
          break;
        case ')':
          result = result * stack.pop() + stack.pop();
          break;
        default:
          int sum = c - '0';
          while (idx < length - 1 && Character.isDigit(s.charAt(idx + 1))) {
            sum = sum * 10 + s.charAt(idx + 1) - '0';
            idx++;
          }
          result += sum * sign;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/579285282/){:target="_blank"}

# 설명
1. 수학 공식을 문자열로 저장한 s를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 주어진 문자열 s를 이용하여 계산된 결과를 넣는 변수이다.
- length는 주어진 문자열 s의 길이를 저장하는 변수이다.
- sign은 덧셈과 뺄셈를 구분하기 위한 변수이다.
- stack은 계산에 필요한 숫자를 저장하기 위해 사용하는 변수이다.

3. 주어진 문자열 s를 이용하여 계산을 진행한다.
- c에 s의 idx번쨰 문자를 넣어준다.
- c가 공백(' ')인 경우, 무시하고 진행한다.
- c가 '+'인 경우, sign에 1을, '-'인 경우에 sign에 -1을 넣어준다.
- c가 '('인 경우, stack에 result와 sign을 넣어주고 result를 0으로 sign은 1로 초기화 한다.
- c가 ')'인 경우, result에 stack에서 꺼낸 값을 곱하고 다음 stack의 값을 더해준다.
- 그 외에는 c가 숫자인 경우이므로, 아래의 계산을 수행한다.
  - sum에 c에 '0'의 ASCII 코드 값을 빼서 숫자를 만들어 넣어준다.
  - idx가 $legnth - 1$ 미만이고, s의 $idx + 1$ 번째 문자가 숫자인 경우 반복하여 sum에 $sum \times 10$에 s의 $idx + 1$ 번째 문자에 '0'의 ASCII 코드 값을 빼서 숫자를 만들어 더한 값을 넣어주고 idx를 증가시킨다.
  - result에 sum에 sign 값을 곱해서 넣어준다.

4. 반복이 완료되면 계산된 결과를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BasicCalculator.java){:target="_blank"}에서 확인 가능합니다.