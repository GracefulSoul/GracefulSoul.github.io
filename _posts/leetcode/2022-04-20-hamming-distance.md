---
title: "Leetcode Java Hamming Distance"
excerpt: "Leetcode Hamming Distance Java 풀이"
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
1. 두 정수 x와 y의 [해밍 거리(Hamming distance)](https://en.wikipedia.org/wiki/Hamming_distance){:target="_blank"}의 수를 구하는 문제이다.

2. 

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HammingDistance.java){:target="_blank"}에서 확인 가능합니다.