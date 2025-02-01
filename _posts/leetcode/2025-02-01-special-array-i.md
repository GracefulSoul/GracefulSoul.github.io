---
title: "Leetcode Java Special Array I"
excerpt: "Leetcode - 'Special Array I' 문제 Java 풀이"
last_modified_at: 2025-02-01T10:30:00
header:
  image: /assets/images/leetcode/special-array-i.png
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
[Link](https://leetcode.com/problems/special-array-i/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isArraySpecial(int[] nums) {
    for (int i = 1; i < nums.length; i++) {
      if (((nums[i - 1] ^ nums[i]) & 1) == 0) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/special-array-i/submissions/1526924367/){:target="_blank"}

# 설명
1. nums 내 붙은 값이 홀수와 짝수가 번갈아 존재하는지 검증하는 문제이다.

2. 1부터 nums의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- num[$i - 1$]의 값과 nums[i]의 값의 XOR(^) 비트 연산 수행한 값과 1의 AND(&) 비트 연산 수행한 값이 0인 경우, false를 주어진 문제의 결과로 반환한다.
  - num[$i - 1$]의 값과 nums[i]의 값의 XOR(^) 비트 연산 수행한 이후 1과 AND(&) 비트 연산을 수행하여 비트 내 1의 자리 값을 가져온다.
  - 위 결과가 이 0인 경우, 동일한 홀수 혹은 짝수가 아닌 경우이므로 false를 반환한다.

3. 반복이 완료되어 검증이 완료되면, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SpecialArrayI.java){:target="_blank"}에서 확인 가능합니다.