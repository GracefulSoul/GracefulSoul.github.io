---
title: "Leetcode Java Preimage Size of Factorial Zeroes Function"
excerpt: "Leetcode Preimage Size of Factorial Zeroes Function Java"
last_modified_at: 2023-01-04T19:50:00
header:
  image: /assets/images/leetcode/preimage-size-of-factorial-zeroes-function.png
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
[Link](https://leetcode.com/problems/preimage-size-of-factorial-zeroes-function){:target="_blank"}

# 코드
```java
class Solution {

  public int preimageSizeFZF(int k) {
    int num = 1;
    while (num < k) {
      num = (num * 5) + 1;
    }
    while (num > 1) {
      k %= num;
      if (num - 1 == k) {
        return 0;
      }
      num = (num - 1) / 5;
    }
    return 5;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/preimage-size-of-factorial-zeroes-function/submissions/871118627/){:target="_blank"}

# 설명
1. 아래의 f(x) 함수를 통해 수행된 결과를 구하는 문제이다.
- f(x)는 x!([Factorial](https://en.wikipedia.org/wiki/Factorial){:target="_blank"}) 값의 마지막에 존재하는 0의 개수가 k인 x의 수이다.
- $f(11) = 2$로, 11!의 결과는 399168<b>00</b>이므로 뒤에 존재하는 0은 2개라는 의미이다.

2. num은 결과를 구하기 위한 임시 값을 생성할 변수로, 1로 초기화 하여 아래를 수행한 결과를 넣어준다.
- num이 k 미만일 때 까지 num에 $(num \times 5) + 1$의 값을 넣어 num을 증가시켜준다.

3. num이 1 초과일 때 까지 아래를 수행한다.
- k를 num으로 나눈 나머지 값을 넣어준다.
- $num - 1$의 값이 k인 경우, f(x)의 결과가 k를 만족하는 x가 존재하지 않으므로 0을 주어진 문제의 결과로 반환한다.
- num에 $\frac{num - 1}{5}$의 몫을 넣어 범위를 좁혀준다.

4. 반복이 정상적으로 종료되면 f(x)의 결과가 k를 만족하는 숫자의 개수인 5를 주어진 문제의 결과로 반환한다.

# 해설
- x!은 $1 \times 2 \times ... \times x$ 이고, x! 결과의 마지막에 0이 k개 존재하는 경우는 10을 만들 수 있는 5의 개수가 k개인 것으로 판단 할 수 있으므로 아래의 각 경우를 확인해보자.
  - k가 0인 경우, 0에서 4까지 5의 배수가 한 개도 없으므로 5개의 숫자가 만족한다.
  - k가 4인 경우, 20에서 24까지 5의 배수가 네 개(5, 10, 15, 20)이므로 5개의 숫자가 만족한다.
  - k가 5인 경우, 25($5 \times 5$)는 5가 두 번 발생하므로 마지막의 0의 수가 5개인 숫자는 없다.
  - k가 6인 경우, 25에서 29까지 5의 배수가 여섯 개(5, 10, 15, 20, 25)이므로 5개의 숫자가 만족한다.
  - k가 10인 경우, 45에서 49까지 5의 배수가 열 개(5, 10, 15, 20, 25, 30, 35, 40, 45)이므로 5개의 숫자가 만족한다.
  - k가 11인 경우, 50($5 \times 5 \times 2$)는 5가 두 번 발생하므로 마지막의 0의 수가 11개인 숫자는 없다.
- 위의 각 경우와 같이 주어진 k 값이 5의 제곱수가 처음 발생하는 구간임이 확인 되면 0, 아니면 5를 반환하는 것이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PreimageSizeOfFactorialZeroesFunction.java){:target="_blank"}에서 확인 가능합니다.