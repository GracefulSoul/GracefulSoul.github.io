---
title: "Leetcode Java Sum of Square Numbers"
excerpt: "Leetcode Sum of Square Numbers Java"
last_modified_at: 2022-08-22T19:30:00
header:
  image: /assets/images/leetcode/sum-of-square-numbers.png
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
[Link](https://leetcode.com/problems/sum-of-square-numbers/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean judgeSquareSum(int c) {
    for (int idx = 2; idx * idx <= c; idx++) {
      int count = 0;
      if (c % idx == 0) {
        while (c % idx == 0) {
          count++;
          c /= idx;
        }
        if (idx % 4 == 3 && count % 2 != 0) {
          return false;
        }
      }
    }
    return c % 4 != 3;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/780201035/){:target="_blank"}

# 설명
1. 음이 아닌 정수 c가 주어졌을 때, $a^2 + b^2 = c$를 만족하는 a와 b가 있는지 검증하는 문제이다.

2. 2부터 $idx^2$이 c 이하인 경우까지 idx를 증가시키며 아래를 반복한다.
- count는 c를 idx로 나눈 횟수를 저장할 변수로, 0으로 초기화한다.
- c와 idx를 나눈 나머지가 0인 경우, 아래를 수행한다.
  - c와 idx를 나눈 나머지가 0이 될 때 까지 반복하여 count를 증가시키고, c에 c와 idx를 나눈 몫을 저장한다.
  - idx와 4를 나눈 나머지가 3이고 count가 홀수인 경우, 주어진 조건을 만족하는 경우가 없으므로 false를 주어진 문제의 결과로 반환한다.

3. 반복이 완료되면 c를 4로 나눈 나머지 값이 3이 아닌지를 검증하여 주어진 문제의 결과로 반환한다.

# 해설
- [페르마의 마지막 정리](https://en.wikipedia.org/wiki/Fermat%27s_Last_Theorem){:target="_blank"}를 이용한 방법으로 n이 3 이상의 정수일 때, $a^n + b^n = c^n$을 만족하는 양의 정수 a, b, c가 존재하지 않는다.
- 위에 따르면 $4k + 3$ 형태의 모든 n의 소인수가 n의 소인수 분해에서 짝수 제곱을 가질 때에만 숫자 n은 두 제곱의 합이므로, 해당 경우에 대한 값의 검증을 수행하면 아래의 각 경우를 수행한다.
  - 반복을 이용하여 c를 4로 나눈 나머지 값이 3이고 짝수 제곱인 경우를 검증하여 먼저 위의 공식에 만족하는 경우를 배제한다.
  - 마지막으로 나머지 값인 c를 4로 나눈 나머지 값이 3이면 동일하게 위의 공식에 만족하는 경우이므로 배제하여 검증 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfSquareNumbers.java){:target="_blank"}에서 확인 가능합니다.