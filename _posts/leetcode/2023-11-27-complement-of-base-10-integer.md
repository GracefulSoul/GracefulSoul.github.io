---
title: "Leetcode Java Complement of Base 10 Integer"
excerpt: "Leetcode Complement of Base 10 Integer Java"
last_modified_at: 2023-11-27T19:40:00
header:
  image: /assets/images/leetcode/complement-of-base-10-integer.png
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
[Link](https://leetcode.com/problems/complement-of-base-10-integer){:target="_blank"}

# 코드
```java
class Solution {

  public int bitwiseComplement(int n) {
    if (n == 0) {
      return 1;
    } else {
      int power = 1;
      while (power <= n) {
        power *= 2;
      }
      return (power - 1) - n;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/complement-of-base-10-integer/submissions/1107356873/){:target="_blank"}

# 설명
1. n의 1의 보수를 구하는 문제이다.

2. n이 0인 경우, 1을 반환한다.

3. 그 외의 경우 power가 n보다 큰 2의 배수로 만들어 1의 보수를 구하는 공식인 $(power - 1) - n$의 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ComplementOfBase10Integer.java){:target="_blank"}에서 확인 가능합니다.