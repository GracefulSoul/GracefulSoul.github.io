---
title: "Leetcode Java Max Area of Island"
excerpt: "Leetcode - 'Max Area of Island' 문제 Java 풀이"
last_modified_at: 2022-10-16T18:00:00
header:
  image: /assets/images/leetcode/max-area-of-island.png
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
[Link](https://leetcode.com/problems/max-area-of-island){:target="_blank"}

# 코드
```java
class Solution {

  public int maxAreaOfIsland(int[][] grid) {
    int max = 0;
    for (int i = 0; i < grid.length; i++) {
      for (int j = 0; j < grid[0].length; j++) {
        if (grid[i][j] == 1) {
          max = Math.max(max, this.dfs(grid, i, j));
        }
      }
    }
    return max;
  }

  private int dfs(int[][] grid, int i, int j) {
    if (i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] != 1) {
      return 0;
    } else {
      int area = 1;
      grid[i][j] = 2;
      area += this.dfs(grid, i - 1, j);
      area += this.dfs(grid, i + 1, j);
      area += this.dfs(grid, i, j - 1);
      area += this.dfs(grid, i, j + 1);
      return area;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/823617190/){:target="_blank"}

# 설명
1. grid 내 섬 중 가장 큰 섬의 면적을 구하는 문제이다.
- gird[i][j]의 값이 0인 경우 해상을, 1인 경우 육지를 의미한다.

2. max는 가장 큰 섬의 면적을 저장할 변수로, 0으로 초기화한다.

3. gird의 모든 값들을 이용하여 gird[i][j]가 1인 경우, 4번에서 정의한 dfs(int[][] grid, int i, int j) 메서드를 이용하여 육지 면적을 계산 후 해당 값과 max 중 큰 값을 max에 넣어준다.

4. 섬의 크기를 계산할 dfs(int[][] grid, int i, int j) 메서드를 정의한다.
- i와 j가 grid의 범위 내에 있으면서, grid의 값이 1인 경우 아래를 수행한다.
  - area에 1을 넣어주고, 현재 위치는 이미 계산에 포함되었으므로 값을 2로 변경해준다.
  - 현재 위치의 4방면의 위치 값을 이용한 재귀 호출 결과를 area에 합해준다.
  - 계산이 완료되면 area를 반환한다.
- 위의 경우가 아니라면 0을 반환한다.

5. 반복이 완료되면 가장 큰 섬의 면적을 저장한 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxAreaOfIsland.java){:target="_blank"}에서 확인 가능합니다.