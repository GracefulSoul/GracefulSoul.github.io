---
title: "Leetcode Java Basic Calculator II"
excerpt: "Leetcode Basic Calculator II Java 풀이"
last_modified_at: 2021-11-02T13:00:00
header:
  image: /assets/images/leetcode/basic-calculator-ii.png
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
[Link](https://leetcode.com/problems/basic-calculator-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int calculate(String s) {
    int sum = 0;
    int pre = 0;
    char sign = '+';
    for (int idx = 0; idx < s.length(); idx++) {
      char c = s.charAt(idx);
      if (c == ' ') {
        continue;
      } else if (Character.isDigit(c)) {
        int num = c - '0';
        while (idx < s.length() - 1 && Character.isDigit(s.charAt(idx + 1))) {
          num = num * 10 + (s.charAt(idx + 1) - '0');
          idx++;
        }
        switch (sign) {
          case '+':
            sum += pre;
            pre = num;
            break;
          case '-':
            sum += pre;
            pre = -num;
            break;
          case '*':
            pre *= num;
            break;
          case '/':
            pre /= num;
            break;
        }
      } else {
        sign = c;
      }
    }
    return sum + pre;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/580763966/){:target="_blank"}

# 설명
1. 지난 번 [Basic Calculator](../basic-calculator){:target="_blank"}와 비슷한 문제로, 사칙연산을 이용한 수학 공식이 담긴 문자열 s를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 사칙 연산의 결과를 저장하기 위한 변수로, 0으로 초기화 시킨다.
- pre는 사칙 연산을 수행할 때 사용되는 두 숫자열 중 앞의 숫자열을 넣어 저장할 변수로, 0으로 초기화 시킨다.
- sign은 사칙 연산에 사용되는 기호를 넣어 저장하는 변수로, '+'로 초기화 시킨다.

3. 문자열 s의 길이만큼 반복하여 계산을 수행한다.

4. s의 idx번째 문자가 ' '(공백)일 경우, 반복을 계속 수행한다.

5. s의 idx번째 문자가 숫자열인 경우, 아래의 계산을 수행한다.
- num에 s의 idx번째 문자를 '0'을 뺀 숫자로 변환한 값을 넣어준다.
- s의 idx번째 문자 이후가 숫자인 경우 반복하여 num에 10을 곱하고, $idx + 1$번째 문자를 '0'을 뺀 숫자로 변환하여 더한 후 idx를 증가시킨다.
- 반복이 완료되면 sign에 따라 값을 넣어준다.
  - '+'인 경우, sum에 pre를 더해주고, pre에 num을 넣어준다.
  - '-'인 경우, sum에 pre를 더해주고, pre에 -num을 넣어준다.
  - '*'인 경우, pre에 num을 곱해준다.
  - '/'인 경우, pre에 num을 나눠준다.

6. 그 외인 경우 사칙연산 기호이기 때문에, sing에 s의 idx번째 문자를 넣어준다.

7. 모든 반복이 완료되면 계산된 결과와 중간 값을 저장한 sum과 pre의 합을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BasicCalculatorII.java){:target="_blank"}에서 확인 가능합니다.