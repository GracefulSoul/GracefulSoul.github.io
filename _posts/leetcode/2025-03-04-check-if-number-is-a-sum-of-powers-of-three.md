---
title: "Leetcode Java Check if Number is a Sum of Powers of Three"
excerpt: "Leetcode - 'Check if Number is a Sum of Powers of Three' 문제 Java 풀이"
last_modified_at: 2025-03-04T22:40:00
header:
  image: /assets/images/leetcode/check-if-number-is-a-sum-of-powers-of-three.png
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
[Link](https://leetcode.com/problems/check-if-number-is-a-sum-of-powers-of-three/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkPowersOfThree(int n) {
    while (n > 0) {
      if (n % 3 == 2) {
        return false;
      }
      n /= 3;
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-number-is-a-sum-of-powers-of-three/submissions/1562385082/){:target="_blank"}

# 설명
1. n을 3의 배수를 최대 한 번씩 사용한 합으로 구성된 숫자인지 검증하는 문제이다.

2. n이 0 초과일 때 까지 아래를 반복한다.
- n을 3으로 나눈 나머지가 2인 3의 공약수가 아닌 3의 배수를 최대 한 번씩 사용하여 구성할 수 없는 숫자인 경우, false를 주어진 문제의 결과로 반환한다.
- n을 3으로 나눈 값을 다시 넣어준다.

3. 반복이 완료되면 주어진 조건을 충족하는 숫자이므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfNumberIsASumOfPowersOfThree.java){:target="_blank"}에서 확인 가능합니다.