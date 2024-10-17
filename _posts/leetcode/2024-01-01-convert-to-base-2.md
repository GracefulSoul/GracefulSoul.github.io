---
title: "Leetcode Java Convert to Base -2"
excerpt: "Leetcode Medium - 'Convert to Base -2' 문제 Java 풀이"
last_modified_at: 2024-01-01T14:00:00
header:
  image: /assets/images/leetcode/convert-to-base-2.png
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
[Link](https://leetcode.com/problems/convert-to-base-2){:target="_blank"}

# 코드
```java
class Solution {

  public String baseNeg2(int n) {
    if (n == 0) {
      return "0";
    }
    StringBuilder sb = new StringBuilder();
    while (n != 0) {
      int num = n % -2;
      n /= -2;
      if (num < 0) {
        num += 2;
        n++;
      }
      sb.append(num);
    }
    return sb.reverse().toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/convert-to-base-2/submissions/1133436551/){:target="_blank"}

# 설명
1. n을 -2진법으로 반환하는 문제이다.

2. n이 0인경우, 0을 주어진 문제의 결과로 반환한다.

3. sb는 동적 문자열 생성에 필요한 변수로, StringBuilder로 초기화한다.

4. n이 0이 아닐 때 까지 -2진수를 표현하기 위해 n을 나누면서 sb에 값을 이어준다.

5. 반복이 완료되면 sb를 역순으로 전환하여 주어진 문제의 결과로 반환한다.

# 참고
[Wikipedia - Negative base](https://en.wikipedia.org/wiki/Negative_base#Calculation){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConvertToBase2.java){:target="_blank"}에서 확인 가능합니다.