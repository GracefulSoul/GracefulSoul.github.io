---
title: "Leetcode Java Knight Dialer"
excerpt: "Leetcode Knight Dialer Java"
last_modified_at: 2023-06-22T18:35:00
header:
  image: /assets/images/leetcode/knight-dialer.png
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
[Link](https://leetcode.com/problems/knight-dialer){:target="_blank"}

# 코드
```java
class Solution {

  public int knightDialer(int n) {
    if (n == 1) {
      return 10;
    }
    int mod = 1000000007;
    int[][] graph = {
      { 4, 6 },
      { 6, 8 },
      { 7, 9 },
      { 4, 8 },
      { 3, 9, 0 },
      {},
      { 1, 7, 0 },
      { 2, 6 },
      { 1, 3 },
      { 2, 4 }
    };
    int[] dp = new int[10];
    Arrays.fill(dp, 1);
    while (n-- > 1) {
      int[] temp = new int[10];
      for (int i = 0; i < graph.length; i++) {
        for (int j = 0; j < graph[i].length; j++) {
          int position = graph[i][j];
          temp[position] = (temp[position] + dp[i] % mod) % mod;
        }
      }
      dp = temp;
    }
    int result = 0;
    for (int num : dp) {
      result = (result + num % mod) % mod;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/knight-dialer/submissions/976989957/){:target="_blank"}

# 설명
1. 체스의 나이트의 이동 경로를 활용하여 숫자 다이얼의 임의 지점에서 시작하여 n길이의 고유한 전화 번호의 수를 구하는 문제이다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. n이 1인 경우, 다이얼의 수인 10을 주어진 문제의 결과로 반환한다.

3. 문제를 풀기 위한 변수를 정의한다.
- mod는 모듈러를 적용할 변수로, $10^9 +7$로 초기화한다.
- graph는 출발 숫자의 위치 별 도착 숫자를 저장할 배열로, 0부터 9까지 위치에서 도착 가능한 위치를 모두 넣어 초기화한다.
- dp는 각 위치 별 전화 번호의 수를 계산할 배열로, 다이얼 수인 10 크기로 정의하고 모든 값을 1로 초기화한다.

4. n이 1 초과일 때 까지 아래를 반복하고 n을 감소시킨다.
- temp는 현재 위치에서 도착 가능한 위치를 저장할 배열로, 다이얼 수인 10 크기로 정의한다.
- 0부터 graph의 길이 미만까지 i를 증가시키고, 0부터 graph의 i번째 길이 미만까지 j를 증가시키며 아래를 반복한다.
  - position에 graph[i][j] 값을 저장한다.
  - temp[position] 위치에 dp[i] 값을 mod로 나눈 값에 temp[position]의 값을 더한 값에 mod로 다시 나눈 값을 넣어준다.
- dp에 temp를 넣고 반복을 계속한다.

5. result는 고유 전화번호의 수를 저장할 변수로, dp의 모든 값을 반복하여 result에 num을 mod로 나눈 나머지와 result를 더한 값에 mod를 나눈 값을 넣어주고 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KnightDialer.java){:target="_blank"}에서 확인 가능합니다.