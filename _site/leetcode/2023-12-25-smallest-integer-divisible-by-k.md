---
title: "Leetcode Java Smallest Integer Divisible by K"
excerpt: "Leetcode Smallest Integer Divisible by K Java"
last_modified_at: 2023-12-25T14:15:00
header:
  image: /assets/images/leetcode/smallest-integer-divisible-by-k.png
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
[Link](https://leetcode.com/problems/smallest-integer-divisible-by-k){:target="_blank"}

# 코드
```java
class Solution {

  public int smallestRepunitDivByK(int k) {
    if (k % 2 == 0 || k % 5 == 0) {
      return -1;
    }
    int result = 0;
    for (int i = 1; i <= k; i++) {
      result = ((result * 10) + 1) % k;
      if (result == 0) {
        return i;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/smallest-integer-divisible-by-k/submissions/1127868157/){:target="_blank"}

# 설명
1. 1로만 이루어진 임의 정수 중 k로 나눌 수 가장 작은 양의 정수를 구하는 문제이다.
- 단, 해당 정수가 존재하지 않으면, -1을 주어진 문제의 결과로 반환한다.

2. k가 2와 5의 약수인 경우 뒷 자리가 1로 끝날 수 없으므로, -1을 주어진 문제의 결과로 반환한다.

3. 값을 저장할 result를 0으로 초기화한다.

4. 1부터 k 이하까지 i를 증가시키며 아래를 수행한다.
- result에 $(result \times 10) + 1$을 수행한 결과를 overflow를 방지하기 위해 k로 나눈 나머지를 넣어준다.
- result가 0이면 나눌 수 있는 값이 존재한다는 의미이므로, 글자 자릿수인 i를 주어진 문제의 결과로 반환한다.

5. 반복이 완료되면 조건에 만족하는 양의 정수가 없으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SmallestIntegerDivisibleByK.java){:target="_blank"}에서 확인 가능합니다.