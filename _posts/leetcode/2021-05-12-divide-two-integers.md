---
title: "Leetcode Java Divide Two Integers"
excerpt: "Leetcode - 'Divide Two Integers' 문제 Java 풀이"
last_modified_at: 2021-05-12T12:40:00
header:
  image: /assets/images/leetcode/divide-two-integers.png
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
[Link](https://leetcode.com/problems/divide-two-integers/){:target="_blank"}

# 코드
```java
class Solution {

  public int divide(int dividend, int divisor) {
    if (dividend == Integer.MIN_VALUE && divisor == -1) {
      return Integer.MAX_VALUE;
    } else {
      return dividend / divisor;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/491571524/){:target="_blank"}

# 설명
1. 주어진 문제에 가장 큰 함정은 최소 값을 -1로 나눈 경우, Integer.MAX_VALUE보다 커진다는 점이다.
- $-2,147,483,648 \times -1 = 2,147,483,648 > 2,147,483,647$ 이므로, 이 경우는 Integer.MAX_VALUE인 $2,147,483,647$을 주어진 문제로 반환한다.

2. 그 외의 경우는 주어진 두 변수를 나눈($\frac{dividned}{divisor}$) 몫을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DivideTwoIntegers.java){:target="_blank"}에서 확인 가능합니다.