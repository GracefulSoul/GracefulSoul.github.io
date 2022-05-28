---
title: "Leetcode Java Fibonacci Number"
excerpt: "Leetcode Fibonacci Number Java"
last_modified_at: 2022-05-27T11:00:00
header:
  image: /assets/images/leetcode/fibonacci-number.png
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
[Link](https://leetcode.com/problems/fibonacci-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int fib(int n) {
    if (n <= 1) {
      return n;
    }
    int pre = 0;
    int curr = 0;
    int result = 1;
    for (int idx = 2; idx <= n; idx++) {
      pre = curr;
      curr = result;
      result = pre + curr;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/708659777/){:target="_blank"}

# 설명
1. [피보나치 수열](https://en.wikipedia.org/wiki/Fibonacci_number){:target="_blank"}의 n번째 숫자를 반환하는 문제이다.

2. n 이 1 이하인 경우 피보나치 수열의 결과와 순번이 동일하므로, n을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- pre는 피보나치 수열의 $n - 2$번째 값을 저장하기 위한 변수이다.
- curr은 피보나치 수열의 $n - 1$번째 값을 저장하기 위한 변수이다.
- result는 피보나치 수열의 n번째 값을 저장하기 위한 변수이다.

4. 2부터 n까지 idx를 증가시키며 피보나치 수열의 값을 계산한다.
- pre에 curr을, curr에 result 값을 넣어준다.
- result는 pre와 curr의 값의 합을 넣어준다.

5. 반복이 완료되면 피보나치 수열의 n번째 값을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FibonacciNumber.java){:target="_blank"}에서 확인 가능합니다.