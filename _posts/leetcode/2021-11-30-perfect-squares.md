---
title: "Leetcode Java Perfect Squares"
excerpt: "Leetcode - 'Perfect Squares' 문제 Java 풀이"
last_modified_at: 2021-11-30T12:00:00
header:
  image: /assets/images/leetcode/perfect-squares.png
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
[Link](https://leetcode.com/problems/perfect-squares/){:target="_blank"}

# 코드
```java
class Solution {

  public int numSquares(int n) {
    for (int idx = 1; idx < n; idx++) {
      if (this.recursive(n, idx)) {
        return idx;
      }
    }
    return n;
  }

  private boolean recursive(int n, int count) {
    if (count == 1) {
      return Math.abs(Math.pow((int) Math.sqrt(n), 2) - n) < 1e-5;
    } else {
      for (int idx = 1; idx * idx <= n; idx++) {
        if (this.recursive(n - idx * idx, count - 1)) {
          return true;
        }
      }
      return false;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/594658661/){:target="_blank"}

# 설명
1. 주어진 정수 n을 이용하여 완전 제곱수의 합으로 해당 값을 이루기 위한 최소 개수를 탐색하는 문제이다.

2. 1부터 n까지 반복하여 n과 idx 값으로 재귀 호출을 활용하여 검증을 수행한다.

3. idx 값이 1인 경우, n의 제곱근의 제곱의 절대 값이 $1 \times E^(-5)$ 미만인 경우 true를 그 외는 false를 반환한다.
- 해당 값의 차이가 큰 경우, n의 제곱근의 값을 이용하여 완전 제곱수를 구성할 수 없기 때문이다.

4. 그 외의 경우, 아래를 진행하여 검증을 수행한다.
- idx를 1부터 시작하여 idx의 제곱의 값이 n 이하일 때 까지 반복한다.
- $n - idx^2$을 n에, count를 감소시켜 재귀 호출을 수행하여 검증한 결과를 확인한다.
  - 재귀 호출로 완전 제곱수를 구성하는 경우, true를 반환한다.
- 반복문이 종료되는 경우 완전 제곱수로 구성이 되지 않는다는 의미이므로, false를 반환한다.

5. 3, 4번의 수행 결과로 true가 반환되면, 완전 제곱수의 최소 개수인 idx를 주어진 문제의 결과로 반환한다.

6. 반복이 모두 완료되면 n은 최소의 완전 제곱수인 1로만 구성된 경우이므로, n을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PerfectSquares.java){:target="_blank"}에서 확인 가능합니다.