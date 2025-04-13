---
title: "Leetcode Java Count Good Numbers"
excerpt: "Leetcode - 'Count Good Numbers' 문제 Java 풀이"
last_modified_at: 2025-04-13T09:50:00
header:
  image: /assets/images/leetcode/count-good-numbers.png
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
[Link](https://leetcode.com/problems/count-good-numbers/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int MOD = 1000000007;

  public int countGoodNumbers(long n) {
    return (int) (this.pow(5, (n + 1) / 2) * this.pow(4, n / 2) % MOD);
  }

  public long pow(long x, long y) {
    if (y == 0) {
      return 1;
    } else {
      long temp = this.pow(x, y / 2);
      if (y % 2 == 0) {
        return (temp * temp) % MOD;
      } else {
        return (x * temp * temp) % MOD;
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-good-numbers/submissions/1605070658/){:target="_blank"}

# 설명
1. n 길이의 숫자들 중 아래의 규칙을 만족하는 좋은 숫자의 갯수를 세는 문제이다.
- 좋은 숫자는 짝수 위치의 값은 짝수이고, 홀수 위치의 값은 소수인 값이다.
- n 길이의 숫자 앞 자리에 0이 포함하여 조건을 만족할 수 있다.
- 조건을 만족하는 숫자의 갯수가 매우 많을 수 있으므로, 모듈러 $10^9 + 7$를 적용하여 반환한다.

2. 조건을 만족하는 제곱을 계산하기 위한 pow(long x, long y) 메서드를 정의한다.
- y가 0인 승수가 0이면, 1을 반환한다.
- y가 0이 아닌 경우, 아래를 수행한다.
  - temp에 x와 $\frac{y}{2}$로 재귀 호출 수행한 결과를 넣어준다.
  - y가 짝수인 경우, $\frac{temp \times temp}{MOD}$를 반환한다.
  - y가 홀수인 경우, $\frac{x \times temp \times temp}{MOD}$를 반환한다.

3. 주어진 조건의 결과로 2번의 pow(long x, long y) 메서드에 5와 $\frac{n + 1}{2}$를 수행한 결과와 4와 $frac{n}{2}$를 수행한 결과의 곱을 주어진 문제의 결과로 반환한다.

# 해설
- 짝수 자리는 짝수인 0, 2, 4, 6, 8 값의 갯수인 5개가, 홀수 자리는 소수인 2, 3, 5, 7 값의 갯수인 4개가 존재한다.
- 좋은 숫자의 총 갯수는 아래의 두 경우의 수에 대한 곱이 되며, 각 계산에 모듈러 $10^9 + 7$을 적용해야 한다.
  - 짝수의 5개에 짝수 인덱스 갯수의 제곱.
  - 소수의 4개에 소수 인덱스 갯수의 제곱.
- 제곱 계산은 승수가 짝수인 경우와 홀수인 경우에 대해서 아래와 같이 계산이 가능하다.
  - y가 짝수인 경우, $x^y = x^\frac{y}{2} \times x^\frac{y}{2}$로 표현 가능하다. 예를 들어, $x^4 = x^2 \times x^2$와 같다.
  - y가 홀수인 경우, $x^y = x \times x^\frac{y}{2} \times x^\frac{y}{2}$로 표현 가능하다. 예를 들어, $x^5 = x \times x^2 \times x^2$와 같다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountGoodNumbers.java){:target="_blank"}에서 확인 가능합니다.