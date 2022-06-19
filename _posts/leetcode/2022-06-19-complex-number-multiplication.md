---
title: "Leetcode Java Complex Number Multiplication"
excerpt: "Leetcode Complex Number Multiplication Java"
last_modified_at: 2022-06-19T17:00:00
header:
  image: /assets/images/leetcode/complex-number-multiplication.png
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
[Link](https://leetcode.com/problems/complex-number-multiplication/){:target="_blank"}

# 코드
```java
class Solution {

  public String complexNumberMultiply(String num1, String num2) {
    int[] num1Array = this.splitNumber(num1);
    int[] num2Array = this.splitNumber(num2);
    return new StringBuilder()
        .append(num1Array[0] * num2Array[0] - num1Array[1] * num2Array[1])
        .append('+')
        .append(num2Array[0] * num1Array[1] + num1Array[0] * num2Array[1])
        .append('i')
        .toString();
  }

  private int[] splitNumber(String num) {
    int index = num.indexOf('+');
    return new int[] { Integer.parseInt(num.substring(0, index)), Integer.parseInt(num.substring(index + 1, num.length() - 1)) };
  }

}
// codec.decode(codec.encode(url));
```

# 결과
[Link](https://leetcode.com/submissions/detail/725611238/){:target="_blank"}

# 설명
1. 복소수를 나타내는 num1과 num2를 곱한 결과를 복소수로 반환하는 문제이다.
- 복소수는 실수 이후 "+" 기호를, 허수 이후 "i"를 붙인 "실수+허수i" 형태로 제공되고 해당 형태로 반환해야 한다.
- 단, $i^2 = -1$이다.

2. 3번에서 정의한 splitNumber(String num) 메서드를 수행하여 num1과 num2의 실수와 허수를 num1Array와 num2Array에 넣어준다.

3. 실수와 허수를 배열로 반환할 splitNumber(String num) 메서드를 정의한다.
- index에 num 위치에 "+" 기호가 있는 위치를 넣어준다.
- num의 처음부터 index까지 값을 숫자로 변환하고, $index + 1$ 위치에서 마지막에서 한 자리 이전 값을 숫자로 변환하여 배열에 넣어 반환한다.

4. num1Array와 num2Array의 결과를 계산하여 StringBuilder로 복소수 형태로 문자열을 만들어 반환한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.
- $"1+1i" \times "1+1i" = (1 + i) \times (1 + i) = 1 + i2 + i^2 = 2i$ 이므로, 아래와 같이 복소수의 각 값을 계산한다.
  - 실수는 $num1Array[0] \times num2Array[0] - num1Array[1] \times num2Array[1]$의 결과로 값을 계산한다.
  - 허수는 $num2Array[0] \times num1Array[1] + num1Array[0] \times num2Array[1]$의 결과로 값을 계산한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ComplexNumberMultiplication.java){:target="_blank"}에서 확인 가능합니다.