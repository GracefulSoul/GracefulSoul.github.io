---
title: "Leetcode Java Soup Servings"
excerpt: "Leetcode Soup Servings Java"
last_modified_at: 2023-01-17T19:20:00
header:
  image: /assets/images/leetcode/soup-servings.png
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
[Link](https://leetcode.com/problems/soup-servings){:target="_blank"}

# 코드
```java
class Solution {

  public double soupServings(int n) {
    n = (n + 24) / 25;
    return n > 500 ? 1.0 : this.dfs(new double[n + 1][n + 1], n, n);
  }

  private double dfs(double[][] dp, int a, int b) {
    if (a <= 0 && b <= 0) {
      return 0.5;
    } else if (a <= 0) {
      return 1;
    } else if (b <= 0) {
      return 0;
    } else if (dp[a][b] > 0) {
      return dp[a][b];
    } else {
      return dp[a][b] = 0.25 * (this.dfs(dp, a - 4, b) + this.dfs(dp, a - 3, b - 1) + this.dfs(dp, a - 2, b - 2) + this.dfs(dp, a - 1, b - 3));
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/soup-servings/submissions/879836198/){:target="_blank"}

# 설명
1. A와 B 스프를 각각 n ml씩 가지고 아래의 네 유형으로 제공할 때, 스프가 하나라도 바닥이 날 때 까지 반복하여 A가 먼저 비어있을 확률과 A와 B가 동시에 비어있을 확률의 절반을 반환한다.
- 단, 결과는 소수점 다섯 자리 이내의 답을 반환한다.
- B 스프 100ml를 모두 먼저 사용하는 경우는 없으며, 유형은 아래의 네 유형으로 존재한다.
  - A 스프 100ml만 제공한다.
  - A 스프 75ml와 B 스프 25ml를 제공한다.
  - A 스프 50ml와 B 스프 50ml를 제공한다.
  - A 스프 25ml와 B 스프 75ml를 제공한다.

2. n에 $\frac{n + 24}{25}$를 넣어 25ml 단위로 산정한 횟수를 넣어준다.

3. n이 192를 초과하는 경우, 해당 경우는 1에 수렴하므로 1.0을 반환하고 아닌 경우 $n + 1$ 크기의 2차원 실수 배열을 이용하여 4번에서 정의한 dfs(double[][] dp, int a, int b) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.
- n이 192인 이유는 아래와 같다.
  - 파라미터로 주어진 초기 n이 4800이면 확률은 0.99999499이고, 4801인 경우 0.99999538으로 4800이 초과되면 반올림하여 1.0에 수렴한다.
  - 4800을 25로 나눈 결과는 192이므로, 해당 결과를 기반으로 산정된 임계치이다.
- 또한 b를 먼저 모두 사용하는 경우는 없으므로, n이 무한히 증가되면 A가 먼저 비어있을 확률은 1에 수렴하게 된다.

4. DFS 방식으로 확률을 계산하기 위한 dfs(double[][] dp, int a, int b) 메서드를 정의한다.
- a와 b가 0 이하인 경우, 둘 다 부족하다는 의미이므로 1의 절반인 0.5를 반환한다.
- a만 0 이하인 경우, 3번에서 설명하였듯이 1을 반환한다.
- b만 0 이하인 경우, 불가능한 경우이므로 0을 반환한다.
- dp[a][b]의 값이 0 초과인 경우, 아직 확률이 존재하므로 해당 값을 반환한다.
- 그 외의 경우, dp[a][b]에 0.25와 스프를 제공하는 네 확률의 합의 곱을 넣고 반환한다.
  - a 스프만 100ml 반환하면 4번 사용하므로 $a - 4$를 이용한 재귀 호출을 수행한 결과를 이용한다.
  - 위와 동일하게 마지막으로 a 스프를 25ml 반환하면 1번, b 스프를 75ml 반환하면 3번 사용하므로 $a - 1$과 $b - 3$을 이용한 재귀 호출을 수행한 결과를 이용한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SoupServings.java){:target="_blank"}에서 확인 가능합니다.