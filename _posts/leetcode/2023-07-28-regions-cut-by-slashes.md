---
title: "Leetcode Java Regions Cut By Slashes"
excerpt: "Leetcode Regions Cut By Slashes Java"
last_modified_at: 2023-07-28T20:20:00
header:
  image: /assets/images/leetcode/regions-cut-by-slashes.png
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
[Link](https://leetcode.com/problems/regions-cut-by-slashes){:target="_blank"}

# 코드
```java
class Solution {

  public int regionsBySlashes(String[] grid) {
    int length = grid.length;
    int size = length * 3;
    int regions = 0;
    int[][] dp = new int[size][size];
    for (int i = 0; i < length; i++) {
      int row = i * 3;
      for (int j = 0; j < length; j++) {
        int col = j * 3;
        if (grid[i].charAt(j) == '/') {
          dp[row][col + 2] = dp[row + 1][col + 1] = dp[row + 2][col] = 1;
        } else if (grid[i].charAt(j) == '\\') {
          dp[row][col] = dp[row + 1][col + 1] = dp[row + 2][col + 2] = 1;
        }
      }
    }
    for (int i = 0; i < size; i++) {
      for (int j = 0; j < size; j++) {
        regions += this.dfs(dp, i, j) > 0 ? 1 : 0;
      }
    }
    return regions;
  }

  private int dfs(int[][] dp, int i, int j) {
    if (Math.min(i, j) < 0 || dp.length <= Math.max(i, j) || dp[i][j] != 0) {
      return 0;
    } else {
      dp[i][j] = 1;
      return 1 + this.dfs(dp, i - 1, j) + this.dfs(dp, i, j - 1) + this.dfs(dp, i + 1, j) + this.dfs(dp, i, j + 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/regions-cut-by-slashes/submissions/1006081526/){:target="_blank"}

# 설명
1. grid는 정사각형의 값을 저장한 변수로, '/'과 '\' 문자열을 이용하여 분리된 사각형 내 영역의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 gird의 길이를 저장한 변수이다.
- size는 영역을 계산하기 위한 dp의 크기를 저장할 변수로, $length \times 3$ 크기로 초기화한다.
- regions는 결과인 영역의 수를 계산하기 위한 변수로, 0으로 초기화한다.
- dp는 regions를 계산하기 위해 구성할 배열로, $size \times size$ 크기의 2차원 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키면서 아래를 수행한다.
- dp 내 행의 시작 위치인 row에 $i \times 3$를 넣어준다.
- 0부터 length 미만까지 j를 증가시키면서 아래를 수행한다.
  - dp 내 열의 시작 위치인 col에 $j \times 3$를 넣어준다.
  - grid의 i번째 행의 j번째 문자가 '/'인 경우, $3 \times 3$크기의 영역 내 좌측 하단부터 우측 상단까지 1을 넣어 구분 선을 그어준다.
  - 위가 아니면서 해당 문자가 '\'인 경우, $3 \times 3$크기의 영역 내 좌측 상단부터 우측 하단까지 1을 넣어 구분 선을 그어준다.

4. 반복이 완료되면 0부터 size까지 i를 증가시키고, 0부터 size까지 j를 증가시키며 regions에 5번에서 정의한 dfs(int[][] dp, int i, int j) 메서드의 수행 결과가 0 초과이면 1 아니면 0을 넣어준다.

5. DFS 방식으로 사각형 내 영역 구분이 이루어지는지 검증하기 위한 dfs(int[][] dp, int i, int j) 메서드를 정의한다.
- i와 j 중 작은 값이 0 미만 혹은 dp의 길이 이상으로 사각형의 범위를 벗어나거나 dp[i][j]의 값이 0이 아닌 값의 경우, 0을 반환한다.
- 위의 경우가 아니라면 dp[i][j]에 1을 넣어주고, 1에 아래의 재귀 호출 결과를 모두 더해 반환한다.
  - $i - 1$과 j를 이용하여 좌측 위치에서 재귀 호출.
  - i와 $j - 1$을 이용하여 하단 위치에서 재귀 호출.
  - $i + 1$과 j를 이용하여 우측 위치에서 재귀 호출.
  - i와 $j + 1$를 이용하여 상단 위치에서 재귀 호출.

6. 모든 반복이 완료되면 영역이 계산된 regions를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RegionsCutBySlashes.java){:target="_blank"}에서 확인 가능합니다.