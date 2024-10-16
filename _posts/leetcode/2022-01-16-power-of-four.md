---
title: "Leetcode Java Power of Four"
excerpt: "Leetcode Power of Four Java 풀이"
last_modified_at: 2022-01-16T16:00:00
header:
  image: /assets/images/leetcode/power-of-four.png
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
[Link](https://leetcode.com/problems/power-of-four/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isPowerOfFour(int n) {
    if ((n & (n - 1)) == 0) {
      while (n > 1) {
        n >>= 2;
      }
    }
    return n == 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/620822861/){:target="_blank"}

# 설명
1. 주어진 정수가 n이 $4^x$인 4의 제곱수인지를 검증하는 문제이다.

2. n과 $n - 1$의 AND(&) 비트 연산의 결과가 0인 경우, n이 1보다 클때까지 반복하여 n의 비트 숫자열을 우측으로 2칸 이동시킨다.
- [Power of Two](../power-of-two){:target="_blank"}와 유사하게 n과 $n - 1$의 AND(&) 비트 연산의 2의 배수의 결과는 0이 된다.
- n의 비트 숫자열을 우측으로 2칸 이동시키면 4를 나눈 상태와 동일하다.

3. n이 1이면 4의 제곱수이므로 true를, 아니면 4의 제곱수가 아니므로 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PowerOfFour.java){:target="_blank"}에서 확인 가능합니다.