---
title: "Leetcode Java Binary Number with Alternating Bits"
excerpt: "Leetcode Binary Number with Alternating Bits Java"
last_modified_at: 2022-10-15T18:00:00
header:
  image: /assets/images/leetcode/binary-number-with-alternating-bits.png
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
[Link](https://leetcode.com/problems/binary-number-with-alternating-bits){:target="_blank"}

# 코드
```java
class Solution {

  public boolean hasAlternatingBits(int n) {
    n ^= (n >> 1);
    return (n & (n + 1)) == 0;
  }


}
```

# 결과
[Link](https://leetcode.com/submissions/detail/822845459/){:target="_blank"}

# 설명
1. 양의 정수인 n이 주어지면 교대로 비트가 존재하는지 검증하는 문제이다.
- 단, 인접한 값들은 항상 10101과 01010과 같이 다른 값을 가져야한다.

2. n의 비트를 오른쪽으로 한 칸 이동하고, 앞의 값과 n과 XOR(^) 비트 연산 결과를 n에 넣어준다.

3. n과 $n + 1$의 AND(&) 비트 연산의 결과가 0인지를 검증한 결과를 주어진 문제의 결과로 반환한다.

# 해설
- n이 5인 경우를 예를 들어보자.
  - 5의 비트 값은 101이므로 비트를 오른쪽으로 한 칸 이동시키면 00101이 된다.
  - 위에서 계산한 값인 010과 n의 비트인 101을 XOR(^) 비트 연산 결과는 111으로, 앞의 값을 n에 넣어준다.
  - 111에 1을 더하면 000이 되므로, 111과 000의 AND(&) 비트 연산 결과는 000인 0이 되어 n은 서로 교차한 값으로 이어진 것이 검증되었다.
- n이 11인 경우를 예를 들어보자.
  - 11의 비트 값은 01011이므로 비트를 오른쪽 한 칸 이동시키면 00101이 된다.
  - 위에서 계산한 값인 00101과 n의 비트인 01011을  XOR(^) 비트 연산 결과는 01110으로, 앞의 값을 n에 넣어준다.
  - 01110에 1을 더하면 01111이 되므로, 01110과 01111의 AND(&) 비트 연산 결과는 01110인 14가 되어 n은 서로 교차한 값으로 이어지지 않은 것이 검증되었다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryNumberWithAlternatingBits.java){:target="_blank"}에서 확인 가능합니다.