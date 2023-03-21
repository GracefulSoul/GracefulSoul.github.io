---
title: "Leetcode Java Nth Magical Number"
excerpt: "Leetcode Nth Magical Number Java"
last_modified_at: 2023-03-20T19:10:00
header:
  image: /assets/images/leetcode/nth-magical-number.png
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
[Link](https://leetcode.com/problems/nth-magical-number){:target="_blank"}

# 코드
```java
class Solution {

  public int nthMagicalNumber(int n, int a, int b) {
    long A = a;
    long B = b;
    long mod = 1000000007L;
    long left = Math.min(a, b);
    long right = (long) n * left;
    while (B > 0) {
      long temp = A;
      A = B;
      B = temp % B;
    }
    long lcm = (a * b) / A;
    while (left < right) {
      long mid = left + (right - left) / 2;
      if ((mid / a) + (mid / b) - (mid / lcm) < n) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return (int) (left % mod);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/nth-magical-number/submissions/918686372/){:target="_blank"}

# 설명
1. a 혹은 b로 나눌 수 있는 n번째 정수를 찾는 문제이다.
- 단, 값이 매우 클 수 있으므로 모듈러 $10^9 + 7$를 이용한 값으로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- A와 B는 주어진 a와 b를 long 형으로 변경한 변수이다.
- mod는 모듈러 $10^9 + 7$ 값을 저장한 변수이다.
- left와 right는 결과 탐색을 수행할 위치 변수로, a와 b 중 가장 작은 값과 해당 값에 n을 더한 값을 각각 넣어준다.

3. B가 0 초과일 때 까지 temp에 A를 임시 보관 후, A에 B를 B에 temp의 B를 나눈 나머지를 넣어준다.

4. lcm은 a와 b의 최소 공배수를 넣을 변수로, $\frac{a \times b}{A}$의 결과를 넣어준다.

5. left가 right보다 작을 때 까지 아래를 반복한다.
- mid는 중앙값을 넣어줄 변수로, $left + \frac{right - left}{2}$를 넣어준다.
- $\frac{mid}{a} + \frac{mid}{b} - \frac{mid}{lcm}$의 결과가 n 미만인 경우, left에 $mid + 1$을 아니면 right에 mid를 넣어 값의 범위를 좁혀준다.

6. 반복이 완료되면 left를 mod로 나눈 값을 int 형으로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NthMagicalNumber.java){:target="_blank"}에서 확인 가능합니다.