---
title: "Leetcode Java Reverse Bits"
excerpt: "Leetcode Reverse Bits Java 풀이"
last_modified_at: 2021-09-30T12:00:00
header:
  image: /assets/images/leetcode/reverse-bits.png
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
[Link](https://leetcode.com/problems/reverse-bits/){:target="_blank"}

# 코드
```java
public class Solution {

  // you need treat n as an unsigned value
  public int reverseBits(int n) {
    int result = 0;
    for (int i = 0; i < 32; i++) {
      result = (result <<= 1) + (n & 1);
      n >>= 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/563240768/){:target="_blank"}

# 설명
1. 주어진 정수 n의 32bit code를 반전한 정수를 구하는 문제이다.

2. 결과를 저장할 result 변수를 0으로 초기화한다.

3. 32번 반복을 통해 주어진 정수 n의 32bit code를 반전시켜 result에 저장한다.
- result의 bit를 좌측으로 한 칸 이동시킨 값과 n과 1의 Bit 논리곱(AND)인 '&'을 이용하여 두 값이 동일하게 1인지를 검증한 결과의 합을 result에 넣어준다.
- n의 bit를 우측으로 한 칸 이동시킨다.

4. 반복이 완료되면 주어진 정수 n의 32bit code를 반전시킨 정수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseBits.java){:target="_blank"}에서 확인 가능합니다.