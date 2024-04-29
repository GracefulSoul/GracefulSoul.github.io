---
title: "Leetcode Java Minimum Number of Operations to Make Array XOR Equal to K"
excerpt: "Leetcode Minimum Number of Operations to Make Array XOR Equal to K Java"
last_modified_at: 2024-04-29T19:30:00
header:
  image: /assets/images/leetcode/minimum-number-of-operations-to-make-array-xor-equal-to-k.png
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
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-xor-equal-to-k/){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(int[] nums, int k) {
    for (int num : nums) {
      k ^= num;
    }
    return Integer.bitCount(k);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-xor-equal-to-k/submissions/1244828555/){:target="_blank"}

# 설명
1. num 내 정수들의 비트를 뒤집어 모든 값들의 XOR 결과가 k가 되기 위한 최소 횟수를 구하는 문제이다.

2. nums의 모든 값을 num에 순차적으로 넣어 k에 k와 num의 XOR(^) 비트 연산을 수행한 결과를 넣어준 후 k의 비트 중 1의 갯수인 뒤집을 최소 횟수를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfOperationsToMakeArrayXOREqualToK.java){:target="_blank"}에서 확인 가능합니다.