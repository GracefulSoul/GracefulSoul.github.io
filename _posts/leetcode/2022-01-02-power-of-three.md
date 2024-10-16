---
title: "Leetcode Java Power of Three"
excerpt: "Leetcode Power of Three Java 풀이"
last_modified_at: 2022-01-02T22:00:00
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
    return n > 0 && 1162261467 % n == 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/611436813/){:target="_blank"}

# 설명
1. 주어진 정수가 n이 $3^x$인 3의 제곱수인지를 검증하는 문제이다.

2. n이 0보다 크고, 1162261467를 n으로 나누었을 때 0인 경우 true를 아니면 false를 반환한다.
- 0은 3의 배수가 아니기 때문에 예외처리를 한다.
- 1162261467는 $3^{19}$로, $3^{20}$은 int형의 자릿수를 벗어나게 되므로 해당 값을 이용하여 n을 나눈 나머지가 0인지를 검증하면 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PowerOfThree.java){:target="_blank"}에서 확인 가능합니다.