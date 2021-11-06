---
title: "Leetcode Java Power of Two"
excerpt: "Leetcode Power of Two Java 풀이"
last_modified_at: 2021-11-06T11:00:00
header:
  image: /assets/images/leetcode/power-of-two.png
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
[Link](https://leetcode.com/problems/power-of-two/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isPowerOfTwo(int n) {
    if (n > 0) {
      return (n & (n - 1)) == 0;
    } else {
      return false;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/582724711/){:target="_blank"}

# 설명
1. 2를 [거듭제곱(Exponentiation)](https://en.wikipedia.org/wiki/Exponentiation){:target="_blank"}하여 나온 결과가 정수 n이 되는지 검증하는 문제이다.
- 단, 반복과 재귀 호출을 사용하지 않고 푸는 방식을 요구한다.

2. n이 0 초과일 경우, 아래의 경우의 따라 주어진 문제의 결과로 반환한다.
- n과 $n - 1$의 AND(&) 비트 연산자의 결과가 0인 경우 true를, 아니면 false를 반환한다.
  - 2의 배수는 2진수로 맨 앞자리가 1이고 뒷자리는 0으로 채워지며, 2의 배수에서 1을 뺀 경우 맨 앞자리가 0이고 뒷자리는 1로 채워지므로 2의 배수와 2의 배수에서 1을 뺀 값의 AND(&) 비트 연산을 수행한 결과는 무조건 0이 될 수 밖에 없다.
  - 간단한 예제로 n이 4인 경우, 4는 2진수로 100, $4 - 1 = 3$이므로 2진수로 011로 표현이 된다.
  - 위의 설명을 토대로 비트 연산을 통해 $100 & 011 = 0$이 된다.

3. n이 0 이하일 경우 2의 거듭제곱으로 표현이 불가능하므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PowerOfTwo.java){:target="_blank"}에서 확인 가능합니다.