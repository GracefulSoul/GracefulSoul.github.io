---
title: "Leetcode Java Binary String With Substrings Representing 1 To N"
excerpt: "Leetcode Medium - 'Binary String With Substrings Representing 1 To N' 문제 Java 풀이"
last_modified_at: 2023-12-28T11:45:00
header:
  image: /assets/images/leetcode/binary-string-with-substrings-representing-1-to-n.png
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
[Link](https://leetcode.com/problems/binary-string-with-substrings-representing-1-to-n){:target="_blank"}

# 코드
```java
class Solution {

  public boolean queryString(String s, int n) {
    for (int i = n; i > n / 2; i--) {
      if (!s.contains(Integer.toBinaryString(i))) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-string-with-substrings-representing-1-to-n/submissions/1130170850/){:target="_blank"}

# 설명
1. [1, n] 범위의 숫자들의 이진 문자열이 모두 s에 부분 문자열인지 검증하는 문제이다.

2. n부터 $\frac{n}{2}$ 이상일 때까지 i를 감소시키며 i의 이진 문자열이 s에 포함되지 않는 경우, 주어진 문제의 결과로 false로 반환한다.
- i < $\frac{n}{2}$를 만족할 때, $i \times 2$의 이진 문자열은 i의 이진 문자열을 모두 포함하기 때문에 [$\frac{n}{2} + 1$, n] 범위의 숫자들만 검증을 수행한다.

3. 반복이 모두 완료되면 모두 포함되므로, 주어진 문제의 결과로 true를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryStringWithSubstringsRepresenting1ToN.java){:target="_blank"}에서 확인 가능합니다.