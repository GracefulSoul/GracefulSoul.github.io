---
title: "Leetcode Java Ugly Number"
excerpt: "Leetcode Ugly Number Java 풀이"
last_modified_at: 2021-11-22T12:00:00
header:
  image: /assets/images/leetcode/ugly-number.png
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
[Link](https://leetcode.com/problems/ugly-number/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isUgly(int n) {
    for (int idx = 2; idx < 6 && n > 0; idx++) {
      while (idx != 4 && n % idx == 0) {
        n /= idx;
      }
    }
    return n == 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/590746728/){:target="_blank"}

# 설명
1. 주어진 정수 n이 못생긴 숫자인지 검증하는 문제이다.
- 못생긴 숫자는 소인수가 2, 3, 5의 숫자로만 구성된 양의 정수이다.

2. 2 ~ 5까지 숫자로 n이 0보다 클 때 까지 반복한다.
- 조건이 2, 3, 5이므로 4를 제외하고 n이 idx를 나눈 나머지 값이 0일 때 까지 반복하여 n을 나누어준다.

3. 반복이 완료되면 n이 1인지를 검증한 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UglyNumber.java){:target="_blank"}에서 확인 가능합니다.