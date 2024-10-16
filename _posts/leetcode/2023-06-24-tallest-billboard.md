---
title: "Leetcode Java Tallest Billboard"
excerpt: "Leetcode Tallest Billboard Java"
last_modified_at: 2023-06-24T10:50:00
header:
  image: /assets/images/leetcode/tallest-billboard.png
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
[Link](https://leetcode.com/problems/tallest-billboard){:target="_blank"}

# 코드
```java
class Solution {

  public int tallestBillboard(int[] rods) {
    int length = rods.length;
    int sum = 0;
    for (int rod : rods) {
      sum += rod;
    }
    int[][] dp = new int[length + 1][sum + 1];
    for (int i = 0; i < length; i++) {
      for (int j = 0; j <= sum; j++) {
        if (dp[i][j] < j) {
          continue;
        }
        dp[i + 1][j] = Math.max(dp[i + 1][j], dp[i][j]);
        int k = j + rods[i];
        dp[i + 1][k] = Math.max(dp[i + 1][k], dp[i][j] + rods[i]);
        k = Math.abs(j - rods[i]);
        dp[i + 1][k] = Math.max(dp[i + 1][k], dp[i][j] + rods[i]);
      }
    }
    return dp[length][0] / 2;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/tallest-billboard/submissions/978215265/){:target="_blank"}

# 설명
1. rods를 이용하여 광고판의 양 쪽을 이어줄 두 지지대를 만들 수 있는 최대 높이를 구하는 문제이다.
- 단, 광고판을 설치할 수 없으면 0을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 rods의 길이를 저장한 변수이다.
- sum은 rods를 모두 이었을 때 최대 길이를 저장할 변수로, rods의 모든 값을 더해서 넣어준다.
- dp는 최대 높이를 구하기 위한 경우의 수를 저장할 변수로, $(length + 1) \times (sum + 1)$ 크기의 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키고, 0부터 sum 이하까지 j를 증가시키며 아래를 수행한다.
- dp[i][j]의 값이 j 미만인 경우, 현재까지 길이보다 짧으므로 다음 반복을 수행한다.
- dp[$i + 1$][j]의 위치에 현재 값과 이전 값인 dp[i][j] 중 큰 값을 넣어준다.
- k에 $j + rods[i]$인 i번째 로드를 이었을 때 길이를 저장하여, dp[$i + 1$][k] 위치에 현재 위치의 값과 이전 위치의 값에 i번째 로드를 더한 값 중 큰 값을 넣어준다.
- k에 $j - rods[i]$인 i번째 로드를 뺀 길이를 넣어 양수로 전환한 값을 저장하고, 위와 동일하게 dp[$i + 1$][k] 위치에 현재 위치의 값과 이전 위치의 값에 i번째 로드를 더한 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 최대 길이가 저장된 dp[length][0]의 값에서 하나의 지지대 길이인 절반을 나누어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TallestBillboard.java){:target="_blank"}에서 확인 가능합니다.