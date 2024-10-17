---
title: "Leetcode Java Profitable Schemes"
excerpt: "Leetcode - 'Profitable Schemes' 문제 Java 풀이"
last_modified_at: 2023-03-21T20:00:00
header:
  image: /assets/images/leetcode/profitable-schemes.png
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
[Link](https://leetcode.com/problems/profitable-schemes){:target="_blank"}

# 코드
```java
class Solution {

  public int profitableSchemes(int n, int minProfit, int[] group, int[] profit) {
    int[][] dp = new int[minProfit + 1][n + 1];
    dp[0][0] = 1;
    int mod = 1000000007;
    for (int k = 0; k < group.length; k++) {
      int g = group[k];
      int p = profit[k];
      for (int i = minProfit; i >= 0; i--) {
        for (int j = n; j >= g; j--) {
          dp[i][j] = (dp[i][j] + dp[Math.max(0, i - p)][j - g]) % mod;
        }
      }
    }
    int result = 0;
    for (int num : dp[minProfit]) {
      result = (result + num) % mod;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/profitable-schemes/submissions/919445645/){:target="_blank"}

# 설명
1. 최소 minProfit의 이익을 낼 수 있는 구성원의 경우의 수를 구하는 문제이다.
- 구성원은 최대 n명까지 설정이 가능하다.
- group[i]는 profix[i]의 이익을 창출한다.
- 경우의 수가 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용하여 결과를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 경우의 수를 구하기 위한 변수로, $(minProfit + 1) \times (n + 1)$ 크기의 2차원 배열로 초기화하고 dp[0][0]에 1을 넣어준다.
- mod는 결과 반환에 사용할 모듈러 값으로, $10^9 + 7$로 초기화한다.

3. k를 0부터 group의 크기까지 k를 증가시키며 아래를 수행한다.
- g에 group의 k번째 값을, p에 profit의 k번째 값을 넣어준다.
- minProfit부터 0 이상까지 i를 감소시키고, n부터 g 이상까지 j를 감소시키며 아래를 수행한다.
  - dp[i][j]번째 위치에 dp[i][j]의 값과 dp 내 0과 $i - p$ 중 큰 값의 행의 $j - g$ 열의 값을 더해서 mod를 나눈 나머지 값을 넣어준다.

4. 반복이 완료되면 경우의 수를 넣을 result에 dp[minProfit] 행의 모든 열 값들을 이용하여 result에 result와 num의 합을 mod로 나눈 나머지 값을 순차적으로 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NthMagicalNumber.java){:target="_blank"}에서 확인 가능합니다.