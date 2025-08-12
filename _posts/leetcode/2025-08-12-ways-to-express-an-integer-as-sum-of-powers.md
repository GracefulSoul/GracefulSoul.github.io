---
title: "Leetcode Java Ways to Express an Integer as Sum of Powers"
excerpt: "Leetcode - 'Ways to Express an Integer as Sum of Powers' 문제 Java 풀이"
last_modified_at: 2025-08-12T18:20:00
header:
  image: /assets/images/leetcode/ways-to-express-an-integer-as-sum-of-powers.png
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
[Link](https://leetcode.com/problems/ways-to-express-an-integer-as-sum-of-powers/){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfWays(int n, int x) {
    int[] dp = new int[n + 1];
    dp[0] = 1;
    int power;
    for (int i = 1; (power = (int) Math.pow(i, x)) <= n; i++) {
      for (int sum = n; power <= sum; sum--) {
        dp[sum] = (dp[sum] + dp[sum - power]) % 1000000007;
      }
    }
    return dp[n];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/submissions/1728505932/){:target="_blank"}

# 설명
1. n을 고유한 양의 정수의 x 제곱의 합으로 표현될 수 있는 방법의 수를 반환하는 문제이다.
- 값이 매우 클 수 있으므로, 모듈러 $10^9 + 7$을 적용하여 계산한다.
- 예를 들어, n = 160이고 x = 3이면 n을 표현하는 방법 중 하나는 $2^3 + 3^3 + 5^3$이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 결과 계산에 사용할 배열로, $n + 1$ 크기의 정수 배열로 초기화하고 첫 값에 1을 넣어준다.
- power는 각 숫자별 제곱 값을 저장할 변수이다.

3. 1부터 $i^x$의 값을 정수로 변환한 power가 n 이하일 때 까지 i를 증가시키며 아래를 반복한다.
- n부터 power가 sum 이하일 때 까지 sum을 감소시키며, dp[sum]의 위치에 아래 두 값의 합을 모듈러 $10^9 + 7$을 적용하여 넣어준다.
  - sum이 되기 위한 경우의 수가 저장된 dp[sum]의 값
  - sum에서 power를 뺀 값을 만들 수 있는 경우의 수인 dp[$sum - power$]의 값

4. 반복이 완료되면 표현될 수 있는 방법의 갯수가 계산된 dp[n]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WaysToExpressAnIntegerAsSumOfPowers.java){:target="_blank"}에서 확인 가능합니다.