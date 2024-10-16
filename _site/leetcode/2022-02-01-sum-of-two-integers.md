---
title: "Leetcode Java Sum of Two Integers"
excerpt: "Leetcode Sum of Two Integers Java 풀이"
last_modified_at: 2022-02-01T20:00:00
header:
  image: /assets/images/leetcode/sum-of-two-integers.png
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
[Link](https://leetcode.com/problems/sum-of-two-integers/){:target="_blank"}

# 코드
```java
class Solution {

  public int getSum(int a, int b) {
    while (a != 0) {
      int carry = (a & b) << 1;
      b = a ^ b;
      a = carry;
    }
    return b;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/632198200/){:target="_blank"}

# 설명
1. 주어진 정수 a와 b의 합을 "+" 혹은 "-" 연산자를 사용하지 않고 두 수의 합을 구하는 문제이다.

2. a가 0이 아닐때 까지 반복한다.
- carry에 a와 b의 AND(&) 비트 연산을 수행하고, 해당 비트를 좌측으로 한 칸 이동시킨다.
- b에 a와 b의 XOR(^) 비트 연산을 수행한 결과를 넣어준다.
- a에 carry를 넣어주고 반복을 계속 한다.

3. 반복이 종료되면 b를 주어진 문제의 결과로 반환한다.

# 예제
- a가 0이고 b가 1인 경우 아래와 같다.
  - a와 b의 AND(&) 비트 연산의 결과는 00 & 01 = 00이다.
  - 00을 좌측으로 1칸 이동시키면, 00 비트는 그대로 carry에 0이 주입된다.
  - a와 b의 XOR(^) 비트 연산의 결과는 00 ^ 01 = 01 = 1으로 b에 주입된다.
  - a에 carry가 들어가 0이므로, 반복이 종료되고 b의 값인 1이 반환된다.
- a가 1이고 b가 2인 경우 아래와 같다.
  - a와 b의 AND(&) 비트 연산의 결과는 01 & 10 = 00이다.
  - 00을 좌측으로 1칸 이동시키면, 00 비트는 그대로 carry에 0이 주입된다.
  - a와 b의 XOR(^) 비트 연산의 결과는 01 ^ 10 = 11 = 3으로 b에 주입된다.
  - a에 carry가 들어가 0이므로, 반복이 종료되고 b의 값인 3이 반환된다.
- 이렇게 AND(&) 비트 연산의 결과를 carry에 넣고, XOR(^) 비트 연산을 이용하여 값을 b에 임시 저장하고, a에 carry를 넣어 반복을 수행하면 "+" 연산과 동일한 결과를 산출한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfTwoIntegers.java){:target="_blank"}에서 확인 가능합니다.