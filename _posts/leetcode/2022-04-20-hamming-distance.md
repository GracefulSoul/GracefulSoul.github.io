---
title: "Leetcode Java Hamming Distance"
excerpt: "Leetcode - 'Hamming Distance' 문제 Java 풀이"
last_modified_at: 2022-04-20T17:00:00
header:
  image: /assets/images/leetcode/hamming-distance.png
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
[Link](https://leetcode.com/problems/hamming-distance/){:target="_blank"}

# 코드
```java
class Solution {

  public int hammingDistance(int x, int y) {
    int bit = x ^ y;
    int count = 0;
    while (bit != 0) {
      bit ^= bit & -bit;
      count++;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/683972909/){:target="_blank"}

# 설명
1. 두 정수 x와 y의 [해밍 거리(Hamming distance)](https://en.wikipedia.org/wiki/Hamming_distance){:target="_blank"}를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- bit는 해밍 거리를 구하기 위한 두 수의 비트의 차이를 넣을 변수로, x와 y의 XOR(^) 비트 연산 결과로 초기화한다.
- count는 해밍 거리를 세기 위한 변수로, 0으로 초기화한다.

3. bit가 0이 아닐 때까지 반복하여 아래를 수행한다.
- bit와 -bit의 AND(&) 비트 연산의 결과와 bit의 XOR(^) 비트 연산의 결과를 bit에 다시 넣어준다.
- 해밍 거리를 저장하는 count를 증가시킨다.

4. 반복이 완료되면 해밍 거리를 저장한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HammingDistance.java){:target="_blank"}에서 확인 가능합니다.