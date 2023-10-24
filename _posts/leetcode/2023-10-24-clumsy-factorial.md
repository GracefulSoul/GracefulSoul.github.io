---
title: "Leetcode Java Clumsy Factorial"
excerpt: "Leetcode Clumsy Factorial Java"
last_modified_at: 2023-10-25T21:20:00
header:
  image: /assets/images/leetcode/clumsy-factorial.png
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
[Link](https://leetcode.com/problems/clumsy-factorial){:target="_blank"}

# 코드
```java
class Solution {

	public int clumsy(int n) {
		switch (n) {
			case 1: case 2: return n;
			case 3: return 6;
			case 4: return 7;
		}
		switch (n % 4) {
			case 1: case 2: return n + 2;
			case 3: return n - 1;
			default: return n + 1;
		}
	}

}
```

# 결과
[Link](https://leetcode.com/problems/clumsy-factorial/submissions/1082957179/){:target="_blank"}

# 설명
1. 아래를 만족하는 공식을 대입하여 값을 구하는 문제이다.
- [Factorial](https://en.wikipedia.org/wiki/Factorial){:target="_blank"}의 함수는 $factorial(n) = n \times (n - 1) \times ... 2 \times 1$의 공식을 수행한다.
- 이를 변조한 clumsy 함수는 $clumsy(n)= n \times (n - 1) / (n - 2) + (n - 3) - ... \times 4 / 3 + 2 - 1$ 형태로 곱하기, 나누기, 더하기, 빼기 순으로 n부터 1까지 수행한 결과를 반환한다.

2. n이 아래의 경우를 만족하면, 각 경우에 대한 값을 주어진 문제의 결과로 반환한다.
- n이 1과 2인 경우, n을 반환한다.
- n이 3인 경우, 6을 반환한다.
- n이 4인 경우, 7을 반환한다.
- n을 4로 나눈 나머지가 1과 2인 경우, $n + 2$를 반환한다.
- n을 4로 나눈 나머지가 3인 경우, $n - 1$을 반환한다.
- 그 외의 경우, $n + 1$을 반환한다.

# 해설
- 고정된 경우인, 1 ~ 4까지는 각 계산의 결과를 반환한다.
- 그 외의 경우, 네 산술 연산자를 수행하는 4가지 경우에 대해서 수행한 결과는 각 수행에 따라 아래와 같은 공식이 성립된다.
  - n을 4로 나눈 나머지가 1인 경우, $clumsy(5) = \frac{5 \times 4}{3} + 2 - 1 = 2$과 같이 $n + 2$이 결과로 산출된다.
  - n을 4로 나눈 나머지가 2인 경우, $clumsy(6) = \frac{6 \times 5}{4} + 3 - (2 \times 1) = 9$아 같이 $n + 1$이 나머지가 1과 동일한 결과로 산출된다.
  - n을 4로 나눈 나머지가 3인 경우, $clumsy(7) = \frac{7 \tiems 6}{5} + 4 - \frac{3 \times 2}{1} = 6$인 $n - 1$이 결과로 산출된다.
  - n을 4로 나눈 나머지가 0인 경우, $clumsy(8) = \frac{8 \times 7}{6} + 5 - \frac{4 \times 3}{2} + 1 = 9$인 $n + 1$이 결과로 산출된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ClumsyFactorial.java){:target="_blank"}에서 확인 가능합니다.