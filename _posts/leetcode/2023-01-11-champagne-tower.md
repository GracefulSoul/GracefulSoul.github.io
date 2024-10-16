---
title: "Leetcode Java Champagne Tower"
excerpt: "Leetcode Champagne Tower Java"
last_modified_at: 2023-01-11T20:30:00
header:
  image: /assets/images/leetcode/champagne-tower.png
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
[Link](https://leetcode.com/problems/champagne-tower){:target="_blank"}

# 코드
```java
class Solution {

  public double champagneTower(int poured, int query_row, int query_glass) {
    double[] dp = new double[101];
    dp[0] = poured;
    for (int row = 1; row <= query_row; row++) {
      for (int col = row; col >= 0; col--) {
        double overflow = (dp[col] - 1) / 2.0;
        overflow = overflow <= 0 ? 0 : overflow;
        dp[col] = overflow;
        dp[col + 1] += overflow;
      }
    }
    return dp[query_glass] >= 1 ? 1 : dp[query_glass];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/champagne-tower/submissions/876069144/){:target="_blank"}

# 설명
1. 첫 번째 줄에 1개의 샴페인 잔으로 시작하여 각 층별 1잔씩 증가시켜 100 번째 줄까지 샴페인으로 된 타워에 1층부터 poured 잔의 샴페인을 부을 경우, query_row번째 줄의 query_glass번째 샴페인잔에 얼마나 많은 양의 샴페인이 차는지를 검증하는 문제이다.
- 첫 번째 줄의 샴페인 잔이 가득 차면, 두 번쨰 줄의 샴페인 잔이 순차적으로 차게 된다.
- 모든 샴페인 잔이 가득 차면, 추가로 부어지는 샴페인은 바닥에 흐르게 된다.

2. dp는 총 100개의 줄로 이루어진 샴페인의 찬 정도를 넣을 배열로, 최대 줄의 크기가 될 수 있도록 101 크기로 초기화하고 첫 값에 poured를 넣어준다.

3. 1부터 query_row 이하까지 row를 증가시키고, row부터 0 이상까지 col을 감소시키며 아래를 반복한다.
- overflow는 넘치는 양의 샴페인을 담을 변수로, dp의 col번째 값에 1을 뺀 값을 2로 나눈 결과를 실수형으로 넣어준다.
- overflow에 overflow가 0 이하면 0을, 아니면 overflow를 넣어준다.
- dp의 col번째 값에 overflow를 넣고, $col + 1$번째 값에 overflow를 더해준다.

4. 반복이 완료되면 dp의 query_glass번째 값이 1 이상이면 1을, 아니면 해당 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ChampagneTower.java){:target="_blank"}에서 확인 가능합니다.