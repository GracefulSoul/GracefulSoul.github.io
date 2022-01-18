---
title: "Leetcode Java Integer Break"
excerpt: "Leetcode Integer Break Java 풀이"
last_modified_at: 2022-01-18T16:00:00
header:
  image: /assets/images/leetcode/integer-break.png
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
[Link](https://leetcode.com/problems/integer-break/){:target="_blank"}

# 코드
```java
class Solution {

  public int integerBreak(int n) {
    if (n <= 3) {
      return n - 1;
    } else {
      int product = 1;
      while (n > 4) {
        product *= 3;
        n -= 3;
      }
      return product * n;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/622218420/){:target="_blank"}

# 설명
1. 주어진 정수 n을 정수의 합으로 표현 가능한 2개 이상의 정수로 쪼갠 숫자들의 곱이 최대인 결과를 찾는 문제이다.

2. n이 3 이하인 경우, 최대가 되는 숫자인 $n - 1$를 주어진 문제의 결과로 반환한다.

3. 2개 이상의 정수로 쪼갠 숫자들의 곱이 최대가 되는 결과를 저장할 product를 정의하고 1로 초기화한다.

4. n이 4보다 클 때까지 반복하여 product에 3을 곱해주고, n에 3을 빼준다.
- n을 3단위로 줄여가며 곱하는 가장 큰 이유는, 6의 경우 $3 \times 3 = 9 > 6 = 2 \times 2 \times 2$, 10의 경우 $3 \times 3 \times 4 = 36 > 25 = 5 \times 5 $로 3 위주의 곱이 가장 큰 결과를 도출 할 수 있다.

5. 반복문이 완료되면 product와 남은 값인 n의 곱을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IntegerBreak.java){:target="_blank"}에서 확인 가능합니다.