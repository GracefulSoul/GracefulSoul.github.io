---
title: "Leetcode Java Calculate Money in Leetcode Bank"
excerpt: "Leetcode Calculate Money in Leetcode Bank Java"
last_modified_at: 2023-12-06T20:20:00
header:
  image: /assets/images/leetcode/calculate-money-in-leetcode-bank.png
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
[Link](https://leetcode.com/problems/calculate-money-in-leetcode-bank){:target="_blank"}

# 코드
```java
class Solution {

  public int totalMoney(int n) {
    int quotient = n / 7;
    int remainder = n % 7;
    return ((28 + remainder) * quotient)
        + (((quotient * (quotient - 1)) / 2) * 7)
        + ((remainder * (remainder + 1)) / 2);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/calculate-money-in-leetcode-bank/submissions/1113534355/){:target="_blank"}

# 설명
1. 아래의 규칙대로 저금하는 경우, n일차에 얼마가 모이는지 계산하는 문제이다.
- 월요일부터 일요일까지 1달러부터 매일 1달러씩 증가하며 저금한다.
  - 월(1), 화(2), 수(3), 목(4), 금(5), 토(6), 일(7)
- 한 주가 넘어가면 그 전주의 월요일보다 1달러 증가시켜 한 주를 다시 저금한다.
  - 2 주차 : 월(2), 화(3), 수(4), 목(5), 금(6), 토(7), 일(8)
  - 3 주차 : 월(3), ..., 일(9)

2. 주 단위를 나타내는 quotient에 $\frac{n}{7}$의 몫을, 한 주가 꽉 차지 않은 나머지 일자를 나타내는 remainder에 나머지를 저장한다.

3. 아래의 계산식을 더한 값을 주어진 문제의 결과로 반환한다.
- 한 주 가중치를 제외한 합과 한 주를 채우지 못한 나머지 요일의 값을 더한 값에 완료된 주차를 곱한 $(28 + remainder) \times quotient$의 결과 값.
- 완료 주에 대한 가중치를 나타내는 $\frac{quotient \tiems (quotient - 1)}{2} \tiems 7$의 결과 값.
- 완료되지 않은 주에 대한 가중치를 나타내는 $\frac{remainder \times (remainder + 1)}{2}$의 결과 값.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CalculateMoneyInLeetcodeBank.java){:target="_blank"}에서 확인 가능합니다.