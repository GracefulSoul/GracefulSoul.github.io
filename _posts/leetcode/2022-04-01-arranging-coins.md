---
title: "Leetcode Java Arranging Coins"
excerpt: "Leetcode Arranging Coins Java 풀이"
last_modified_at: 2022-04-01T17:00:00
header:
  image: /assets/images/leetcode/arranging-coins.png
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
[Link](https://leetcode.com/problems/arranging-coins/){:target="_blank"}

# 코드
```java
class Solution {

  public int arrangeCoins(int n) {
    long left = 0;
    long right = n;
    while (left <= right) {
      long mid = left + (right - left) / 2;
      long curr = mid * (mid + 1) / 2;
      if (n < curr) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    }
    return (int) right;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/671499742/){:target="_blank"}

# 설명
1. 정수 n이 주어지면 동전으로 계단을 만들 경우, 만들어진 완전한 계단의 층수를 반환하는 문제이다.
- 계단은 우측에서 좌측으로 올라가는 형태로 구성이 된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- left는 좌측 포인터 역할을 수행할 변수로 overflow를 방지하기 위해서 long으로 정의하고, 0으로 초기화한다.
- right는 우측 포인터 역할을 수행할 변수로 overflow를 방지하기 위해서 long으로 정의하고, n으로 초기화한다.

3. left가 right보다 작거나 같을 때 까지 아래를 반복한다.
- 중간 값을 지정할 mid를 $left + \frac{right - left}{2}$로 정의한다.
- 현재 포인터 역할을 수행할 curr을 $\frac{mid \times (mid + 1)}{2}$로 정의한다.
- n이 curr보다 작은 경우, right에 $mid - 1$을 넣어 탐색 범위를 축소시킨다.
- n이 curr보다 크거나 같은 경우, left에 $mid + 1$을 넣어 탐색 범위를 축소시킨다.

4. 반복이 완료되면 최종 포인터의 위치인 right를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ArrangingCoins.java){:target="_blank"}에서 확인 가능합니다.