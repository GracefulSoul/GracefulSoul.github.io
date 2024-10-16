---
title: "Leetcode Java Number of Digit One"
excerpt: "Leetcode Number of Digit One Java 풀이"
last_modified_at: 2021-11-08T12:00:00
header:
  image: /assets/images/leetcode/number-of-digit-one.png
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
[Link](https://leetcode.com/problems/number-of-digit-one/){:target="_blank"}

# 코드
```java
class Solution {

  public int countDigitOne(int n) {
    int result = 0;
    for (int unit = 1; unit <= n; unit *= 10) {
      int quotient = n / unit;
      int remainder = n % unit;
      result += (((quotient + 8) / 10) * unit) + (quotient % 10 == 1 ? remainder + 1 : 0);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/583711666/){:target="_blank"}

# 설명
1. 주어진 정수 n 이하의 정수에 포함되는 숫자 1의 개수를 구하는 문제이다.

2. 숫자 1이 포함되는 개수를 저장하기 위한 변수 result를 정의하고 0으로 초기화한다.

3. 1부터 n 이하의 10의 승수로 반복하여 1의 개수를 산정한다.
- 몫을 저장할 quotient에 $\frac{n}{unit}$의 값을, 나머지를 저장할 remainder에 n을 unit으로 나눈 나머지 값을 넣어준다.
- result에 $(((quotient + 8) / 10) * unit) + (quotient % 10 == 1 ? remainder + 1 : 0)$ 값을 더해준다.
  - $((quotient + 8) / 10) * unit$에서 위의 값에서 10을 나눈 값에 unit을 곱하는 이유는, unit의 단위(10의 승수) 별 1의 개수를 산정하기 위한 로직이다.
  - $quotient + 8$를 하는 이유는 n이 20 이후의 숫자인 경우, 10 ~ 19까지의 1의 개수인 10개를 보정하기 위한 로직이다.
  - $quotient % 10 == 1 ? remainder + 1 : 0$는 11와 같은 특수 행의 경우 1의 개수를 추가 산정하기 위해 $remainder + 1$의 결과를 더해주는 것이다.

4. 반복이 완료되면 주어진 정수 n 이하의 정수에 포함되는 숫자 1의 개수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfDigitOne.java){:target="_blank"}에서 확인 가능합니다.