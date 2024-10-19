---
title: "Leetcode Java Find Kth Bit in Nth Binary String"
excerpt: "Leetcode - 'Find Kth Bit in Nth Binary String' 문제 Java 풀이"
last_modified_at: 2024-10-19T20:10:00
header:
  image: /assets/images/leetcode/find-kth-bit-in-nth-binary-string.png
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
[Link](https://leetcode.com/problems/find-kth-bit-in-nth-binary-string/){:target="_blank"}

# 코드
```java
class Solution {

  public char findKthBit(int n, int k) {
    int flips = 0;
    while (n > 1) {
      int length = (1 << n) - 1;
      int mid = (length + 1) / 2;
      if (k == mid) {
        return flips == 0 ? '1' : '0';
      } else if (k > mid) {
        flips ^= 1;
        k = length - k + 1;
      }
      n -= 1;
    }
    return flips == 0 ? '0' : '1';
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-kth-bit-in-nth-binary-string/submissions/1426923165/){:target="_blank"}

# 설명
1. n을 이용하여 아래의 규칙대로 수행하였을 때, k번쨰 비트 문자를 반환하는 문제이다.
- S<sub>0</sub> = 0 으로 시작하여, S<sub>i</sub> = S<sub>i - 1</sub> + "1" + reverse(invert(S<sub>i - 1</sub>))를 만족한다.
- invert(x)는 x의 비트의 값을 1은 0으로, 0은 1로 반전시키는 역할을 수행하는 함수이다.
- reverse(x)는 x의 비트 값을 뒤에서 앞으로 반전 시키는 열할을 수행하는 함수이다.

2. flips는 반전시키는 횟수를 계산하기 위한 변수로, 0으로 초기화한다.

3. n이 1 초과일 때까지 아래를 반복한다.
- 반복에 필요한 변수를 정의한다.
  - length는 길이를 계산하기 위한 변수로, 1의 비트를 n번 좌측으로 이동시킨 후 1을 감소시킨다.
  - mid는 중앙 값을 저장할 변수로, $\frac{length + 1}{2}$의 값을 넣어준다.
- k가 mid인 목표 지점이면서 flips가 홀수인 경우, 기본 문자열인 '1'을 아니면 '0'을 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니면서 k가 mid보다 큰 경우, flips에 1의 XOR('^') 비트연산의 결과를 넣어주고, k에 $length - k + 1$인 값을 넣어준다.
- n을 감소시키고 다음 반복을 수행한다.

4. 반복이 완료되면 flips가 짝수인 경우, '0'을 아니면 '1'을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindKthBitInNthBinaryString.java){:target="_blank"}에서 확인 가능합니다.