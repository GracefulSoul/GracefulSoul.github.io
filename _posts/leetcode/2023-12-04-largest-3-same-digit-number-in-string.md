---
title: "Leetcode Java Largest 3-Same-Digit Number in String"
excerpt: "Leetcode Largest 3-Same-Digit Number in String Java"
last_modified_at: 2023-12-04T20:50:00
header:
  image: /assets/images/leetcode/largest-3-same-digit-number-in-string.png
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
[Link](https://leetcode.com/problems/largest-3-same-digit-number-in-string){:target="_blank"}

# 코드
```java
class Solution {

  public String largestGoodInteger(String num) {
    int result = -1;
    for (int i = 2; i < num.length(); i++) {
      if (num.charAt(i - 2) == num.charAt(i) && num.charAt(i - 1) == num.charAt(i)) {
        result = Math.max(result, num.charAt(i) - '0');
      }
    }
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < 3; i++) {
      sb.append((char) (48 + result));
    }
    return result == -1 ? "" : sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-3-same-digit-number-in-string/submissions/1112121154/){:target="_blank"}

# 설명
1. num내 3개의 연속된 숫자가 동일한 값들 중 가장 큰 값을 찾는 문제이다.
- 조건에 맞는 값이 없는 경우, ""를 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 num내 3개의 연속된 숫자가 동일한 값들 중 큰 값을 넣을 변수로, nums를 반복하여 세 값이 동일한 문자열의 가장 큰 숫자의 위치를 넣어준다.
- sb는 동적으로 문자를 만들 변수로, StringBuilder로 초기화한다.

3. 0부터 3 미만까지 i를 증가시키며 sb에 해당 숫자를 문자로 변환하여 이어준다.

4. result가 -1인 경우 ""을, 값이 존재하는 경우 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Largest3SameDigitNumberInString.java){:target="_blank"}에서 확인 가능합니다.