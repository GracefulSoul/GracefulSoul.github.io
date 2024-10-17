---
title: "Leetcode Java Stone Game II"
excerpt: "Leetcode - 'Stone Game II' 문제 Java 풀이"
last_modified_at: 2023-05-26T19:45:00
header:
  image: /assets/images/leetcode/stone-game-ii.png
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
[Link](https://leetcode.com/problems/stone-game-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int stoneGameII(int[] piles) {
    int length = piles.length;
    for (int i = length - 2; i >= 0; i--) {
      piles[i] += piles[i + 1];
    }
    return this.dfs(piles, new int[length][length], 1, 0);
  }

  private int dfs(int[] piles, int[][] dp, int m, int p) {
    if (p + 2 * m >= piles.length) {
      return piles[p];
    } else if (dp[p][m] > 0) {
      return dp[p][m];
    } else {
      int result = 0;
      for (int i = 1; i <= 2 * m; i++) {
        result = Math.max(result, piles[p] - this.dfs(piles, dp, Math.max(i, m), p + i));
      }
      dp[p][m] = result;
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/stone-game-ii/submissions/957628567/){:target="_blank"}

# 설명
1. 지난 번 [Stone Game](../stone-game){:target="_blank"}과 비슷하게, 아래 규칙대로 돌을 빼앗는 게임을 수행하여 얻을 수 있는 엘리스의 돌의 최대 갯수를 구하는 문제이다.
- 일렬로 정렬된 여러 개의 말뚝의 각 위치에 piles[i]개의 돌이 있다.
- m은 1로 엘리스와 밥 순서대로 서로 번갈아 시작한다.
- 1 <= X <= 2M를 만족하는 말뚝에 존재하는 X개의 돌을 가져가고 M에 M과 X 중 큰 값을 넣어준다.

2. length는 piles의 길이를 저장한 변수로, $length - 2$부터 0 이상까지 i를 감소시키며 piles의 i번째 위치에 $i + 1$번째 값을 더해준다.

3. 4번에서 정의한 dfs(int[] piles, int[][] dp, int m, int p) 메서드를 dp에 $length \times length$ 크기의 정수 배열과 m과 p에 1과 0을 이용하여 수행한 결과를 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 돌의 수를 탐색할 dfs(int[] piles, int[][] dp, int m, int p) 메서드를 수행한다.
- $p + 2 \times m$의 결과가 piles의 길이보다 크거나 같은 경우, piles의 p의 위치에 해당하는 값을 반환한다.
- 위의 경우가 아니면서 dp[p][m]의 값이 0보다 큰 경우, 이미 수행된 결과이므로 해당 값을 반환한다.
- 위의 모든 경우가 아니라면 아래를 수행한다.
  - result는 돌의 수를 저장하기 위한 변수로 0으로 초기화한다.
  - 1부터 $2 \times m$ 이하까지 i를 증가시키며 result에 result와 piles[p]에 m에 i와 m 중 큰 값과 p에 $p + i$를 이용하여 재귀 호출한 결과를 넣어준다.
  - dp[p][m]의 위치에 result를 넣고, result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StoneGameII.java){:target="_blank"}에서 확인 가능합니다.