---
title: "Leetcode Java Neighboring Bitwise XOR"
excerpt: "Leetcode - 'Neighboring Bitwise XOR' 문제 Java 풀이"
last_modified_at: 2025-01-17T18:30:00
header:
  image: /assets/images/leetcode/neighboring-bitwise-xor.png
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
[Link](https://leetcode.com/problems/neighboring-bitwise-xor/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean doesValidArrayExist(int[] derived) {
    int sum = 0;
    for (int derive : derived) {
      sum += derive;
    }
    return sum % 2 == 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/neighboring-bitwise-xor/submissions/1511343939/){:target="_blank"}

# 설명
1. [0, $n - 1$] 범위 값을 가진 길이 n인 derived 정수 배열을 이용하여 아래를 만족하는 배열이 존재하는지 여부를 검증하는 문제이다.
- i = $n - 1$인 경우, derived[i] = original[i] ^ original[0]를 만족한다.
- 위의 경우가 아닌 경우, derived[i] = original[i] ^ original[$i + 1$]를 만족한다.

2. derived의 합계가 짝수인지의 여부를 주어진 문제의 결과로 반환한다.
- 조건에 만족하기 위한 기본 논제를 정리한다.
  - derived = [A[0], A[1], ..., A[$n - 1$]] = [A[0] ^ A[1], A[1] ^ A[2], ..., A[n-1] ^ A[0]]을 만족한다.
  - 조건에 따른 derived의 값은 (A[0] ^ A[1]) ^ (A[1] ^ A[2]) ^  ... ^ (A[$n - 1$] ^ A[0]) = 0을 만족한다.
  - 위에 따라 SUM(derived) 의 결과가 짝수인지가 주어진 조건을 만족하는 경우이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NeighboringBitwiseXOR.java){:target="_blank"}에서 확인 가능합니다.