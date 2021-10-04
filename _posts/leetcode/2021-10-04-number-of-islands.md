---
title: "Leetcode Java Number of Islands"
excerpt: "Leetcode Number of Islands Java 풀이"
last_modified_at: 2021-10-04T10:00:00
header:
  image: /assets/images/leetcode/number-of-islands.png
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
[Link](https://leetcode.com/problems/number-of-islands/){:target="_blank"}

# 코드
```java
public class Solution {

  public int numIslands(char[][] grid) {
    int result = 0;
    for (int i = 0; i < grid.length; i++)
      for (int j = 0; j < grid[0].length; j++) {
        if (grid[i][j] == '1') {
          this.dfs(grid, i, j);
          result++;
        }
      }
    return result;
  }

  private void dfs(char[][] grid, int i, int j) {
    if (i >= 0 && j >= 0 && i < grid.length && j < grid[0].length && grid[i][j] == '1') {
      grid[i][j] = '0';
      this.dfs(grid, i + 1, j);
      this.dfs(grid, i - 1, j);
      this.dfs(grid, i, j + 1);
      this.dfs(grid, i, j - 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/565337868/){:target="_blank"}

# 설명
1. 주어진 2차원 배열 grid를 이용하여 섬의 갯수를 구하는 문제이다.
- grid는 바다를 '0'으로 육지를 '1'로 표현하며, 인접하지 않은 '1'은 섬을 의미한다.

2. 주어진 grid를 반복하여 섬의 갯수를 구한다.
- grid[i][j]의 값이 1인 경우, 배열 내 인접한 육지인 '1'을 바다인 '0'로 변경하고 result를 증가시킨다.

3. 반복이 완료되면 섬의 갯수를 저장한 변수 result의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfIslands.java){:target="_blank"}에서 확인 가능합니다.