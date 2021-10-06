---
title: "Leetcode Java Happy Number"
excerpt: "Leetcode Happy Number Java 풀이"
last_modified_at: 2021-10-06T12:00:00
header:
  image: /assets/images/leetcode/happy-number.png
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
[Link](https://leetcode.com/problems/happy-number/){:target="_blank"}

# 코드
```java
public class Solution {

  public boolean isHappy(int n) {
    Set<Integer> set = new HashSet<>();
    int sum = 0;
    while (set.add(n)) {
      sum = 0;
      while (n > 0) {
        sum += Math.pow(n % 10, 2);
        n /= 10;
      }
      if (sum == 1) {
        return true;
      } else {
        n = sum;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/566500165/){:target="_blank"}

# 설명
1. 주어진 정수 n의 각 자릿수의 제곱을 더한 값을 앞의 방식대로 계속 수행했을 경우, 1이 되는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- set은 n의 각 자릿수의 제곱을 더한 값이 반복되는지 확인하기 위한 변수이다.
- sum은 각 자릿수의 제곱을 더한 값을 임시 저장하는 변수이다.

3. set에 n을 넣었을 경우, 중복되지 않았을 경우 아래를 반복한다.
- sum을 0으로 초기화 하고, 각 자릿수의 제곱을 sum에 더하고 n을 10으로 나눈 값을 n에 다시 넣어준다.
- sum이 1인 경우, 주어진 문제의 결과로 true를 반환한다.
- sum이 1이 아닌 경우, n에 sum을 넣고 반복을 계속 수행한다.

4. 반복이 종료된 경우 반복된 값이 계속 발생하는 경우이므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HappyNumber.java){:target="_blank"}에서 확인 가능합니다.