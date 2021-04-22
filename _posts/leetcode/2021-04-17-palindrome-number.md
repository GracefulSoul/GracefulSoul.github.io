---
title: "Leetcode Java Palindrome Number"
excerpt: "Leetcode Palindrome Number Java 풀이"
last_modified_at: 2021-04-17T12:50:00
header:
  image: /assets/images/leetcode/palindrome-number.png
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
[Link](https://leetcode.com/problems/palindrome-number/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isPalindrome(int x) {
    if (x < 0 || (x != 0 && x % 10 == 0)) {
      return false;
    } else {
      int reverse = 0;
      while (x > reverse) {
        reverse = reverse * 10 + x % 10;
        x /= 10;
      }
      return x == reverse || x == reverse / 10;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/481574918/){:target="_blank"}

# 설명
1. 주어진 정수 x가 만일 0보다 작거나 10의 배수인 경우, 주어진 문제의 결과로 false를 반환한다.
  - 음수의 경우는 false로 반환하는 예외로 문제에 명시되어있다.
  - 10의 배수를 false 처리하는 이유는 결과가 특정 값 기준으로 좌우가 같을 경우를 제외하였다. (Ex. 121, 12321)

2. 주어진 정수를 절반으로 나누어 반대로 저장시킬 reverse 변수를 선언하고 reverse 변수가 x보다 더 크거나 같을 때 까지 반복한다.
  - 주어진 정수 x의 절반을 반대로 전환시키면 해당 정수가 회문 정수형인지 확인 가능하다.
  - 만일 주어진 정수 x가 1221이라면, x가 12이고 reverse가 12일 때 까지 반복한다.
  - 만일 주어진 정수 x가 12321이라면, x가 12이고 reverse가 123일 때 까지 반복한다.
  - 마지막으로 x를 10으로 나눈 몫을 x에 다시 주입한다.

3. 주어진 정수 x의 절반과 반대로 저장시킨 reverse 변수의 값이 동일하거나 $\frac{reverse}{10}$와 동일하면 true로, 아니면 false로 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PalindromeNumber.java){:target="_blank"}에서 확인 가능합니다.