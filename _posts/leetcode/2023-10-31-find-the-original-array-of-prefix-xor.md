---
title: "Leetcode Java Find The Original Array of Prefix Xor"
excerpt: "Leetcode Find The Original Array of Prefix Xor Java"
last_modified_at: 2023-10-31T19:10:00
header:
  image: /assets/images/leetcode/find-the-original-array-of-prefix-xor.png
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
[Link](https://leetcode.com/problems/find-the-original-array-of-prefix-xor){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findArray(int[] pref) {
    for (int i = pref.length - 1; i > 0; i--) {
      pref[i] ^= pref[i - 1];
    }
    return pref;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-original-array-of-prefix-xor/submissions/1088254568/){:target="_blank"}

# 설명
1. pref 내 값들을 pref[i] = pref[0] ^ pref[1] ^ ... ^ pref[i]를 만족하는 배열로 만들어 반환하는 문제이다.
- '^' 연산자는 XOR 비트 연산자이다.

2. $pref.length - 1$부터 0초과일 때 까지 i를 감소하며, pref[i]에 자신의 값과 pref[$i - 1$]의 값으로 XOR 비트 연산을 수행한 값을 넣어준다.

3. 각 위치 별 XOR 연산을 수행하여 완성된 pref 배열을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheOriginalArrayOfPrefixXor.java){:target="_blank"}에서 확인 가능합니다.