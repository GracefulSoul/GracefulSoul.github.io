---
title: "Leetcode Java Minimize XOR"
excerpt: "Leetcode - 'Minimize XOR' 문제 Java 풀이"
last_modified_at: 2025-01-15T17:50:00
header:
  image: /assets/images/leetcode/minimize-xor.png
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
[Link](https://leetcode.com/problems/minimize-xor/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimizeXor(int num1, int num2) {
    int bit1 = Integer.bitCount(num1);
    int bit2 = Integer.bitCount(num2);
    int result = num1;
    for (int i = 0; i < 32; i++) {
      if (bit1 > bit2 && ((1 << i) & num1) > 0) {
        result ^= 1 << i;
        bit1--;
      }
      if (bit1 < bit2 && ((1 << i) & num1) == 0) {
        result ^= 1 << i;
        bit1++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimize-xor/submissions/1509193463/){:target="_blank"}

# 설명
1. 양의 정수 num1과 num2를 이용하여 아래의 규칙을 만족하는 양의 정수를 구하는 문제이다.
- 결과를 만족하는 양의 정수는 num2와 동일한 비트 수를 가지고 있다.
- 결과를 만족하는 양의 정수와 num1의 XOR(^) 비트 연산의 결과는 최솟값이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- bit1과 bit2는 num1과 num2의 비트 값이 1인 갯수를 넣은 변수이다.
- result에는 num1을 넣어준다.

3. int의 범위 내인 0부터 32 미만까지 i를 증가시키면서 아래를 반복한다.
- bit1이 bit2보다 크면서 1을 i번 좌측으로 비트를 이동시킨 값과 num1의 AND(&) 비트 연산의 결과가 0보다 큰 경우, result에 1을 i번 좌측으로 이동시킨 값과 자기 자신의 값을 XOR(^) 비트 연산 수행한 결과를 넣고 bit1을 감소시켜 비트 수를 조율한다.
- bit1이 bit2보다 작으면서 1을 i번 좌측으로 비트를 이동시킨 값과 num1의 AND(&) 비트 연산의 결과가 0인 경우, result에 1을 i번 좌측으로 이동시킨 값과 자기 자신의 값을 XOR(^) 비트 연산 수행한 결과를 넣고 bit1을 증가시켜 비트 수를 관율한다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimizeXOR.java){:target="_blank"}에서 확인 가능합니다.