---
title: "Leetcode Java Unique Paths III"
excerpt: "Leetcode Hard - 'Unique Paths III' 문제 Java 풀이"
last_modified_at: 2023-08-23T18:45:00
header:
  image: /assets/images/leetcode/unique-paths-iii.png
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
[Link](https://leetcode.com/problems/unique-paths-iii){:target="_blank"}

# 코드
```java
class Solution {

  public int uniquePathsIII(int[][] grid) {
    int count = 0;
    int x = 0;
    int y = 0;
    for (int i = 0; i < grid.length; i++) {
      for (int j = 0; j < grid[0].length; j++) {
        if (grid[i][j] == 0) {
          count++;
        } else if (grid[i][j] == 1) {
          x = i;
          y = j;
        }
      }
    }
    return this.dfs(grid, x, y, count);
  }

  private int dfs(int[][] grid, int x, int y, int count) {
    if (x < 0 || y < 0 || x >= grid.length || y >= grid[0].length || grid[x][y] == -1) {
      return 0;
    } else if (grid[x][y] == 2) {
      return count == -1 ? 1 : 0;
    } else {
      grid[x][y] = -1;
      count--;
      int total = this.dfs(grid, x + 1, y, count) + this.dfs(grid, x, y + 1, count) + this.dfs(grid, x - 1, y, count) + this.dfs(grid, x, y - 1, count);
      grid[x][y] = 0;
      count++;
      return total;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/unique-paths-iii/submissions/1029419087/){:target="_blank"}

# 설명
1. grid 내 1의 위치에서 2의 위치까지 -1이 있는 칸을 피해 0이 존재하는 칸을 모두 지나갈 수 있는 경우의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 0의 갯수를 계산하기 위한 변수로, 0으로 초기화한다.
- x와 y는 시작 위치를 저장할 변수로, 0으로 초기화한다.

3. grid의 모든 값을 이용하여 count에 0인 칸의 갯수를, x와 y에 1의 위치를 넣어준다.

4. 5번에서 정의한 dfs(int[][] grid, int x, int y, int count) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

5. DFS 방식으로 경우의 수를 계산하기 위한 dfs(int[][] grid, int x, int y, int count) 메서드를 정의한다.
- x와 y가 grid 범위를 넘어가거나, -1인 방해물인 경우 0을 반환한다.
- 위의 경우가 아니면서 grid[x][y]의 값이 2인 도착지인 경우, count가 -1이면 1을 아니면 0을 반환한다.
- 위의 모든 경우가 아니라면 아래르 수행한다.
  - grid[x][y]에 -1을 넣어 지나간 기록을 남기고 count를 감소시킨다.
  - total에 [x, y]의 우측, 위, 좌측, 아래 순으로 재귀 호출을 수행한 결과를 더해서 넣어준다.
  - grid[x][y]에 0을 넣어 초기화하고 count를 증가시킨 후 total을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniquePathsIII.java){:target="_blank"}에서 확인 가능합니다.