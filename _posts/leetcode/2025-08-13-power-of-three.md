---
title: "Leetcode Java Power of Three"
excerpt: "Leetcode - 'Power of Three' 문제 Java 풀이"
last_modified_at: 2025-08-13T18:30:00
header:
  image: /assets/images/leetcode/power-of-three.png
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
[Link](https://leetcode.com/problems/power-of-three/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isPowerOfThree(int n) {
    if (n <= 0) {
      return false;
    } else {
      while (n % 3 == 0) {
        n /= 3;
      }
      return n == 1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/1733532865/){:target="_blank"}

# 설명
1. 주어진 정수가 n이 $3^x$인 3의 제곱수인지를 검증하는 문제이다.

2. n이 0 이하인 3의 제곱수로 표현 불가능한 값인 경우, false를 주어진 문제의 결과로 반환한다.

3. n을 나머지 값이 0이 아닐 때 까지 3으로 계속 나눈 나머지 값이 1인 3으로만 구성되는지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PowerOfThree.java){:target="_blank"}에서 확인 가능합니다.