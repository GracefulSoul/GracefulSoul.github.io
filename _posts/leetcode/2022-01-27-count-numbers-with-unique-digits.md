---
title: "Leetcode Java Count Numbers with Unique Digits"
excerpt: "Leetcode Count Numbers with Unique Digits Java 풀이"
last_modified_at: 2022-01-27T17:00:00
header:
  image: /assets/images/leetcode/count-numbers-with-unique-digits.png
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
[Link](https://leetcode.com/problems/count-numbers-with-unique-digits/){:target="_blank"}

# 코드
```java
class Solution {

  public int countNumbersWithUniqueDigits(int n) {
    if (n == 0) {
      return 1;
    } else {
      int count = 10;
      int unit = 9;
      for (int idx = 2; idx <= n && idx <= 10; idx++) {
        unit *= 9 - idx + 2;
        count += unit;
      }
      return count;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/628883641/){:target="_blank"}

# 설명
1. 주어진 정수 n을 이용하여 0 이상 $10^{n}$미만의 고유한 숫자로 이루어진 숫자열의 갯수를 찾는 문제이다.

2. n이 0인 경우 0밖에 없으므로, 1을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- count는 n이 1인 경우 0 ~ 9 까지 10개의 고유 숫자가 존재하므로, 10으로 초기화 한다.
- unit은 유일한 숫자의 갯수를 산정하기 위한 초기 단위이다.

4. 2부터 idx가 n과 10 이하일 때까지 증가시키며 숫자를 센다.
- unit에 $9 - idx + 2$와 자기 자신을 곱한 후, count에 더하여 반복을 계속 수행한다.
  - n이 2인 경우, $10 + (9 \times 9) = 10 + 81 = 91$이 고유한 숫자들로 이루어진 숫자열의 갯수이다.
  - n이 3인 경우, $10 + (9 \times 9) + (9 \times 9 \times 8) = 10 + 81 + 648 = 739$이 고유한 숫자들로 이루어진 숫자열의 갯수이다.
  - 이런 식으로 0이상 $10^{n}$ 미만의 고유한 숫자들로 이루어진 숫자열의 갯수를 구할 수 있다.

5. 총 갯수를 계산한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountNumbersWithUniqueDigits.java){:target="_blank"}에서 확인 가능합니다.