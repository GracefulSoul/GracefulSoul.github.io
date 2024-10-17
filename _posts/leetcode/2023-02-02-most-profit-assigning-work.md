---
title: "Leetcode Java Most Profit Assigning Work"
excerpt: "Leetcode - 'Most Profit Assigning Work' 문제 Java 풀이"
last_modified_at: 2023-02-02T19:50:00
header:
  image: /assets/images/leetcode/most-profit-assigning-work.png
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
[Link](https://leetcode.com/problems/most-profit-assigning-work){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProfitAssignment(int[] difficulty, int[] profit, int[] worker) {
    int[] dp = new int[100001];
    for (int idx = 0; idx < difficulty.length; idx++) {
      dp[difficulty[idx]] = Math.max(dp[difficulty[idx]], profit[idx]);
    }
    for (int idx = 1; idx < dp.length; idx++) {
      dp[idx] = Math.max(dp[idx - 1], dp[idx]);
    }
    int result = 0;
    for (int ability : worker) {
      result += dp[ability];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/most-profit-assigning-work/submissions/889993698/){:target="_blank"}

# 설명
1. 난이도에 해당하는 difficulty별 작업자인 worker를 배치하여 얻을 수 있는 수익인 profit을 이용하여 최대 이익을 구하는 문제이다.
- 작업자 별 최대 하나 이상의 작업을 할당할 수 있으며, 한 작업을 여러 번 수행할 수 있다.

2. dp는 이익을 계산하기 위한 배열로, 최대 정수 범위인 100000보다 1 큰 크기로 초기화하고 아래를 수행한다.
- 0부터 difficulty의 길이 미만까지 idx를 증가시키며, dp의 difficulty 내 idx번째 위치에 해당 값과 profix의 idx번째 값 중 큰 값을 넣어준다.

3. 1부터 dp의 길이 미만까지 idx를 증가시키며, dp의 idx번째 값에 이전 위치의 값과 현재 값 중 큰 값을 넣어준다.

4. result는 최대 이익을 저장하기 위한 변수로, 0으로 초기화하고 worker의 모든 값을 이용하여 dp 내 각 작업자별 이익을 result에 더하고 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MostProfitAssigningWork.java){:target="_blank"}에서 확인 가능합니다.