---
title: "Leetcode Java Prime Number of Set Bits in Binary Representation"
excerpt: "Leetcode - 'Prime Number of Set Bits in Binary Representation' 문제 Java 풀이"
last_modified_at: 2022-12-13T10:00:00
header:
  image: /assets/images/leetcode/prime-number-of-set-bits-in-binary-representation.png
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
[Link](https://leetcode.com/problems/prime-number-of-set-bits-in-binary-representation){:target="_blank"}

# 코드
```java
class Solution {

  public int countPrimeSetBits(int left, int right) {
    Set<Integer> primes = new HashSet<>(Arrays.asList(2, 3, 5, 7, 11, 13, 17, 19));
    int count = 0;
    for (int idx = left; idx <= right; idx++) {
      int bits = 0;
      for (int n = idx; n > 0; n >>= 1) {
        bits += n & 1;
      }
      if (primes.contains(bits)) {
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/prime-number-of-set-bits-in-binary-representation/submissions/858894488/){:target="_blank"}

# 설명
1. left에서 right까지 각 숫자를 이진수로 표현할 때 1의 개수가 소수인 숫자의 개수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- primes는 소수를 넣어 저장할 변수로, 2 ~ 19까지 소수를 넣어 저장한다.
  - left와 right의 범위는 $1 <= left <= right <= 10^6$ 이다.
  - $10^6 = (10^3)^2 < (2^{10})^2 = 2^{20}$를 만족하므로 이진수로 변환할 경우의 최대 길이는 20이다.
  - 그렇기 때문에 20 이상의 소수는 저장할 필요가 없으므로, 19까지 넣어준다.
- count는 이진 표현법 내 소수인 숫자의 개수를 저장할 변수로, 0으로 초기화한다.

3. left부터 right까지 idx를 증가시키며 아래를 반복한다.
- bits는 1의 개수를 저장할 변수로, 0으로 초기화한다.
- idx부터 0 초과일때 까지 n의 비트를 우측으로 하나씩 이동시키며 bits에 1의 개수를 저장한다.
- primes에 bits가 포함되는 경우, count를 증가시킨다.

4. 반복이 완료되면 조건을 만족하는 숫자의 개수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PrimeNumberOfSetBitsInBinaryRepresentation.java){:target="_blank"}에서 확인 가능합니다.