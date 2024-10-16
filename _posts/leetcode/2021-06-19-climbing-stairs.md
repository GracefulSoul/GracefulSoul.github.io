---
title: "Leetcode Java Climbing Stairs"
excerpt: "Leetcode Climbing Stairs Java 풀이"
last_modified_at: 2021-06-19T17:00:00
header:
  image: /assets/images/leetcode/climbing-stairs.png
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
[Link](https://leetcode.com/problems/climbing-stairs/){:target="_blank"}

# 코드
## Use Loop
```java
class Solution {

  public int climbStairs(int n) {
    int result = 1;
    for (int idx = 0, diff = 0; idx < n; idx++) {
      result += diff;
      diff = result - diff;
    }
    return result;
  }

}
```

## Use Array
```java
class Solution {

  public int climbStairs(int n) {
    int[] fibonacci = new int[n + 1];
    fibonacci[0] = 1;
    fibonacci[1] = 2;
    for (int idx = 2; idx < n; idx++) {
      fibonacci[idx] = fibonacci[idx - 2] + fibonacci[idx - 1];
    }
    return fibonacci[n - 1];
  }

}
```

# 결과
[Link(Use Loop)](https://leetcode.com/submissions/detail/510029589/){:target="_blank"}
[Link(Use Array)](https://leetcode.com/submissions/detail/510033864/){:target="_blank"}

# 설명
1. 주어진 정수 n을 1과 2의 조합으로 만들수 있는 고유 숫자열의 개수를 구하는 문제이다.

2. 패턴을 파악해보면 아래와 같은 피보나치 수열로 구성되는 것을 확인 할 수 있다.
- 1 : 1 -> 1
- 2 : 11 2 -> 2
- 3 : 111 12 21 -> 3
- 4 : 1111 112 121 211 22 -> 5 
- 5 : 11111 1112 1121 1211 2111 122 212 221 -> 8
- 6 : 111111 11112 11121 11211 12111 21111 1122 1212 1221 2112 2121 2211 222 -> 13
- 7 : 1111111 111112 111121 111211 112111 121111 211111 11122 11212 11221 12112 12121 12211 21112 21121 21211 22111 1222 2122 2212 2221 -> 21

3. Loop를 사용하여 결과를 구한 첫 번째 코드는 피보나치 수열의 기본적인 개념을 사용한 것이다.
- 피보나치 수열로 구해진 결과를 저장할 result를 1로 초기화하여 정의한다.
- 주어진 정수 n의 크기만큼 반복하여 고유 숫자열의 개수를 구한다.
- result는 diff값을 계속 더해주고, diff는 직전 값을 보관하기 위하여 $result - diff$ 값을 저장한다.
- 반복이 완료되면 고유 숫자열의 개수인 result를 주어진 문제의 결과로 반환한다.

4. Array를 사용하여 결과를 구한 두 번째 코드는 피보나치 수열을 그대로 구현하여 사용한 것이다.
- 피보나치 수열을 저장할 배열 fibonacci를 주어진 정수 n을 이용하여 $n + 1$로 정의한다.
  - 크기가 n이 아니라 $n + 1$로 하는 이유는 주어진 정수 n이 1일 경우, 배열의 초기 값인 1과 2를 추가할 때 ArrayIndexOutOfBoundsException이 발생하기 때문이다.
- 2 ~ $n - 1$번까지 반복하여 fibonacci 배열을 구성한다.
- 반복이 완료되면 fibonacci[$n - 1$] 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ClimbingStairs.java){:target="_blank"}에서 확인 가능합니다.