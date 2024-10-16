---
title: "Leetcode Java Minimum One Bit Operations to Make Integers Zero"
excerpt: "Leetcode Minimum One Bit Operations to Make Integers Zero Java"
last_modified_at: 2023-11-30T20:10:00
header:
  image: /assets/images/leetcode/minimum-one-bit-operations-to-make-integers-zero.png
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
[Link](https://leetcode.com/problems/minimum-one-bit-operations-to-make-integers-zero){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumOneBitOperations(int n) {
    int result = 0;
    int sign = 1;
    while (n > 0) {
      result += (n ^ (n - 1)) * sign;
      sign = -sign;
      n &= n - 1;
    }
    return Math.abs(result);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-one-bit-operations-to-make-integers-zero/submissions/1109526430/){:target="_blank"}

# 설명
1. 정수 n을 아래의 규칙을 이용하여 0으로 변환하는데 필요한 최소 작업 수를 구하는 문제이다.
- n의 이진 표현에서 가장 우측 비트를 변경한다.
- n의 이진 표현에서 $i - 1$번째 비트가 1일 때, $i - 2$번째 부터 가장 우측에 있는 비트가 0으로 설정된 경우 i번째 비트를 변경한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최소 작업의 수를 저장할 변수로, 0으로 초기화한다.
- sign은 최소 작업의 수를 계산하기 위한 변수로, 1로 초기화한다.

3. n이 0 초과일 때까지 아래를 수행한다.
- result에 n과 $n - 1$의 XOR(^) 비트 연산 수행 결과와 sign의 곱을 더해준다.
- sign의 부호를 반전시켜준다.
- n에 n과 $n - 1$과 AND(&) 비트 연산을 수행한 결과를 넣어, n의 이진 표현에서 가장 좌측에 존재하는 1의 위치를 다음 1의 위치로 이동한다.

4. 반복이 완료되면 최소 작업의 수가 계산된 result의 절댓값을 주어진 문제의 결과로 반환한다.

# 해설
- i번째 위치만 1인 값을 0으로 변환하기 위한 과정은 아래와 같다.
  - 1 -> 0 = 1
  - 2 -> 0 = 3
  - 4 -> 0 = 7
- 위의 결과를 통해 $2^i$를 0으로 변환하기 위한 과정은 $2^(i + 1) - 1 =$ n ^ ($n - 1$)의 공식을 얻을 수 있다.
- 이를 이용하여 각 위치를 계산하기 위해서는 위치 별 값에 대해서 n ^ ($n - 1$)의 값을 빼주어야 한다.
  - 예를 들어 n이 6인 경우, $110 = 2^3 - 1 - (2^2 - 1) = $3 ^ 2 - 2 ^ 1$ = 7 - 3 = 4$ 가 된다.
- 결과인 result는 각 경우를 지속 차감하여 음수로 전환될 수 있지만, 부호를 제외한 단순 횟수로는 동일하므로 절댓값을 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumOneBitOperationsToMakeIntegersZero.java){:target="_blank"}에서 확인 가능합니다.