---
title: "Leetcode Java Minimum Score Triangulation of Polygon"
excerpt: "Leetcode Minimum Score Triangulation of Polygon Java"
last_modified_at: 2024-03-07T19:00:00
header:
  image: /assets/images/leetcode/minimum-score-triangulation-of-polygon.png
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
[Link](https://leetcode.com/problems/minimum-score-triangulation-of-polygon){:target="_blank"}

# 코드
```java
class Solution {

  public int minScoreTriangulation(int[] values) {
    int length = values.length;
    int[][] dp = new int[length][length];
    for (int[] row : dp) {
      Arrays.fill(row, -1);
    }
    return this.dfs(values, dp, 1, length - 1);
  }

  private int dfs(int[] values, int[][] dp, int i, int j) {
    if (i >= j) {
      return 0;
    } else if (dp[i][j] != -1) {
      return dp[i][j];
    } else {
      int min = Integer.MAX_VALUE;
      for (int k = i; k < j; k++) {
        min = Math.min(min, this.dfs(values, dp, i, k) + this.dfs(values, dp, k + 1, j) + values[i - 1] * values[k] * values[j]);
      }
      return dp[i][j] = min;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-score-triangulation-of-polygon/submissions/1196611636/){:target="_blank"}

# 설명
1. 주어진 values의 길이보다 2 작은 갯수의 삼각형을 만들 때, 각 꼭짓점의 값들을 values의 값을 대입하여 각 삼각형 내 모든 꼭짓점의 값들을 곱한 값을 더한 값이 최소가 되는 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 values의 길이를 저장한 변수이다.
- dp는 각 삼각형 내 모든 꼭짓점의 값들을 곱한 값을 더한 값이 최소가 되는 값을 구하기 위한 변수로, $length \times length$ 크기의 2차원 정수 배열로 초기화 후 모든 값에 -1을 넣어준다.

3. 4번에서 정의한 dfs(int[] values, int[][] dp, int i, int j) 메서드의 i에 1을, j에 $length - 1$을 넣어 수행하여 탐색한 최솟값을 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 최소 값을 탐색할 dfs(int[] values, int[][] dp, int i, int j) 메서드를 정의한다.
- i가 j보다 큰 탐색 범위를 벗어나는 경우, 0을 반환한다.
- 위의 경우가 아니면서 dp[i][j]의 값이 -1이 아닌 탐색한 위치인 경우, 해당 값을 반환한다.
- 위의 모든 경우가 아니라면 아래를 수행한다.
  - min에 정수의 최댓값을 넣어준다.
  - k가 i부터 j 미만일 때까지 k를 증가시키면서, min에 i와 j의 위치에 i와 k, $k + 1$과 j를 넣어 재귀 호출을 수행한 값에 각 꼭짓점의 값을 곱한 값과 min 중 작은 값을 넣어준다.
  - dp[i][j]의 위치에 min을 넣어준 후, 해당 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumScoreTriangulationOfPolygon.java){:target="_blank"}에서 확인 가능합니다.