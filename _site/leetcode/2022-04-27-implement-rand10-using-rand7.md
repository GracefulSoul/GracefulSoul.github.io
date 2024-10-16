---
title: "Leetcode Java Implement Rand10() Using Rand7()"
excerpt: "Leetcode Implement Rand10() Using Rand7() Java 풀이"
last_modified_at: 2022-04-27T09:00:00
header:
  image: /assets/images/leetcode/implement-rand10-using-rand7.png
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
[Link](https://leetcode.com/problems/implement-rand10-using-rand7/){:target="_blank"}

# 코드
```java
/**
 * The rand7() API is already defined in the parent class SolBase.
 * public int rand7();
 * @return a random integer in the range 1 to 7
 */
class Solution extends SolBase {

  public int rand10() {
    while (true) {
      int num = (7 * (super.rand7() - 1)) + super.rand7();
      if (num <= 40) {
        return (num % 10) + 1;
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/688169066/){:target="_blank"}

# 설명
1. 1 ~ 7까지 균등한 임의 정수를 반환하는 rand7() API가 주어지면, 해당 API만 활용하여 1 ~ 10까지 균등한 임의 정수를 반환하는 rand10() 메서드를 완성하는 문제이다.

2. 아래를 만족하여 결과를 반환하기 전까지 계속 반복을 수행한다.
- num에 $7 \times (super.rand7() - 1) + super.rand7()$의 결과를 넣어준다.
  - $rand7() - 1$은 0 ~ 6까지의 정수가 가능하며, 7을 곱해주면 0 ~ 42까지 정수가 가능하다.
  - 위의 값에 rand7()의 결과를 더하면 0 ~ 49까지 정수로 이루어질 수 있다.
- num의 결과가 40 이하인 경우, $\frac{num}{10} + 1$ 결과를 반환한다.
  - 0 ~ 49까지 정수를 10으로 나눈 나머지는 0 ~ 9로 이루어지며, 1을 더해주면 균등한 확률의 1 ~ 10까지 정수로 생성된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ImplementRand10UsingRand7.java){:target="_blank"}에서 확인 가능합니다.