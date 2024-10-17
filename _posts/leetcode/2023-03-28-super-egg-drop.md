---
title: "Leetcode Java Super Egg Drop"
excerpt: "Leetcode - 'Super Egg Drop' 문제 Java 풀이"
last_modified_at: 2023-03-28T23:10:00
header:
  image: /assets/images/leetcode/super-egg-drop.png
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
[Link](https://leetcode.com/problems/super-egg-drop){:target="_blank"}

# 코드
```java
class Solution {

  public int superEggDrop(int k, int n) {
    int[][] dp = new int[n + 1][k + 1];
    int i = 0;
    while (dp[i][k] < n) {
      i++;
      for (int j = 1; j <= k; j++) {
        dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j] + 1;
      }
    }
    return i;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/super-egg-drop/submissions/923645751/){:target="_blank"}

# 설명
1. k개 달걀을 이용하여 [1, n] 높이의 건물에서 달걀이 깨지지 않는 높이인 f를 찾는 최소 단계를 구하는 문제이다.
- 0 <= f <= n 인 바닥 f보다 높은 위치에서 떨어트린 달걀은 깨지며, f보다 낮은 위치에서 떨어트린 달걀은 깨지지 않는다.
- 계란이 깨지지 않은 경우, 다음 시도에 다시 사용할 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 최소 단계를 찾기 위한 배열로, $(n + 1) \times (k + 1)$ 크기의 2차원 정수 배열로 초기화한다.
- i는 최소 단계를 찾을 변수로, 0으로 초기화한다.

3. dp[i][k]의 값이 n 미만일 때까지 아래를 반복한다.
- i를 증가시키고, 1부터 k 이하까지 j를 증가시키며 아래를 반복한다.
  - dp[i][j]의 위치에 dp[$i - 1$][$j - 1$] 층을 탐색한 값과 dp[$i - 1$][j] 층을 탐색한 값의 합에 1을 더한 값을 넣어 단계를 증가시킨다.

4. 반복이 완료되면 최소 단계인 i를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SuperEggDrop.java){:target="_blank"}에서 확인 가능합니다.