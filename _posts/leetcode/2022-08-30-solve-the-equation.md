---
title: "Leetcode Java Solve the Equation"
excerpt: "Leetcode Solve the Equation Java"
last_modified_at: 2022-08-30T20:10:00
header:
  image: /assets/images/leetcode/solve-the-equation.png
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
[Link](https://leetcode.com/problems/solve-the-equation/){:target="_blank"}

# 코드
```java
class Solution {

  public String solveEquation(String equation) {
    String[] split = equation.split("=");
    int[] values = new int[4];
    this.caculate(split[0], values, 0);
    this.caculate(split[1], values, 2);
    int left = values[0] - values[2];
    int right = values[3] - values[1];
    if (left == 0 && right == 0) {
      return "Infinite solutions";
    } else if (left == 0) {
      return "No solution";
    } else {
      return new StringBuilder("x=").append(right / left).toString();
    }
  }

  private void caculate(String s, int[] values, int index) {
    int sign = 1;
    int value = 0;
    char prev = '1';
    for (char c : s.toCharArray()) {
      if (c == 'x') {
        if (value == 0 && (prev != '0')) {
          value = 1;
        }
        values[index] += sign * value;
        value = 0;
      } else if (c == '+' || c == '-') {
        values[index + 1] += sign * value;
        value = 0;
        sign = (c == '+') ? 1 : -1;
      } else {
        value = (value * 10) + (c - '0');
      }
      prev = c;
    }
    values[index + 1] += sign * value;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/787084478/){:target="_blank"}

# 설명
1. x에 대한 방정식을 문자열로 저장한 equation을 계산하는 문제이다.
- 방정식의 풀이가 불가능한 경우, "No solution"을 반환한다.
- x의 값이 무한히 가능한 경우, "Infinite solutions"을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- split은 equation을 "=" 기준으로 분리한 문자 배열을 저장한다.
- values는 방정식의 값들을 저장할 배열로, 좌변과 우변의 x와 상수 값을 차례대로 3번에서 정의한 caculate(String s, int[] values, int index) 메서드를 이용하여 넣어준다.

3. 방정식의 좌변과 우변의 값을 정리하기 위한 caculate(String s, int[] values, int index) 메서드를 정의한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - sign은 양수와 음수를 구분하기 위한 변수로, 1로 초기화한다.
  - value는 계산한 값을 저장하기 위한 변수로, 0으로 초기화한다.
  - prev는 이전 값을 저장하기 위한 임시 변수로 ,1로 초기화한다.
- s의 모든 문자를 c로 처음부터 끝까지 아래를 이용하여 반복한다.
  - c가 'x'인 경우, value가 0이고 prev가 '0'이 아니면 value를 1로 초기화 후 values의 index번째 위치에 $sign \times value$의 결과를 더하고 value를 0으로 초기화한다.
  - c가 '+'이거나 '-'인 경우, values의 $index + 1$번째 위치에 $sign \times value$를 더하고 value를 0으로 초기화 후 sign을 c가 '+'이면 1로, 아니면 -1로 초기화한다.
  - 그 외의 경우 value에 $value \times 10$에 c를 숫자로 변환한 값을 더한 결과를 넣어 value의 자릿수를 증가시킨다.
- 반복이 완료되면 values의 $index + 1$번째 위치에 $sign \times value$를 더해 마무리한다.

4. 방정식 형태의 값을 계산한다.
- 방정식 내 x의 값을 저장할 left에 values의 0번째 값과 2번째 값의 차이를 넣어준다.
- 방정식 내 상수의 값을 저장할 right에 value의 3번째 값과 1번째 값의 차이를 넣어준다.
- 예를 들어 $2x + 1 = x + 2$인 경우, $x = 1$로 만들어준다.

5. 아래의 경우를 검증하여 주어진 문제의 결과를 반환한다.
- left와 right가 0이면 $0x = 0$이므로 x는 무한한 값이 가능하므로, "Infinite solutions"를 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니면서 left만 0인 경우 $0x = 1$이므로 방정식 풀이가 불가능하므로, "No solution"을 주어진 문제의 결과로 반환한다.
- 위의 경우들이 아니면, "x=" 다음 값에 $\frac{right}{left}$인 결과를 더해 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SolveTheEquation.java){:target="_blank"}에서 확인 가능합니다.