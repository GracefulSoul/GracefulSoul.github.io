---
title: "Leetcode Java Rotting Oranges"
excerpt: "Leetcode Medium - 'Rotting Oranges' 문제 Java 풀이"
last_modified_at: 2023-09-17T15:20:00
header:
  image: /assets/images/leetcode/rotting-oranges.png
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
[Link](https://leetcode.com/problems/rotting-oranges){:target="_blank"}

# 코드
```java
class Solution {

  public int orangesRotting(int[][] grid) {
    for (int i = 0; i < grid.length; i++) {
      for (int j = 0; j < grid[0].length; j++) {
        if (grid[i][j] == 2) {
          this.dfs(grid, i, j, 2);
        }
      }
    }
    int minutes = 2;
    for (int[] row : grid) {
      for (int col : row) {
        if (col == 1) {
          return -1;
        }
        minutes = Math.max(minutes, col);
      }
    }
    return minutes - 2;
  }

  private void dfs(int[][] grid, int i, int j, int minutes) {
    if (i >= 0 && i < grid.length && j >= 0 && j < grid[0].length && grid[i][j] != 0 && (grid[i][j] == 1 || grid[i][j] >= minutes)) {
      grid[i][j] = minutes;
      this.dfs(grid, i - 1, j, minutes + 1);
      this.dfs(grid, i + 1, j, minutes + 1);
      this.dfs(grid, i, j - 1, minutes + 1);
      this.dfs(grid, i, j + 1, minutes + 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/rotting-oranges/submissions/1051571224/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 grid를 이용하여 신선한 오렌지가 없어질 때 까지 걸리는 시간(분)을 반환하는 문제이다.
- grid 내 값은 아래를 의미한다.
  - 0은 빈 셀을 의미한다.
  - 1은 신선한 오렌지를 의미한다.
  - 2는 썩은 오렌지를 의미한다.
- 매 시간(분) 마다 썩은 오렌지의 4 방향에 존재하는 신선한 오렌지는 썩게된다.
- 신선한 오렌지를 모두 썩게할 수 없다면 -1을 반환한다.

2. 0부터 grid.length 미만까지 i를, 0부터 grid[0].length 미만까지 j를 증가시키며 grid[i][j]의 값이 2인 썩은 오렌지이면 3번에서 정의한 dfs(int[][] grid, int i, int j, int minutes) 메서드를 수행한다.

3. DFS 방식으로 신선한 오렌지가 썩을 때 까지 걸리는 시간을 구하기 위한 dfs(int[][] grid, int i, int j, int minutes) 메서드를 정의한다.
- 아래의 조건에 모두 해당하는 경우, 현재 위치에서 4 방향으로 minutes를 1 증가시켜 재귀 호출을 수행한다.
  - i와 j가 그리드 내 범위에 있는 경우.
  - gird[i][j]의 값이 0이 아닌 경우.
  - grid[i][j]의 값이 1인 신선한 오렌지이거나, minutes 이상인 소요 시간(분)이 현재 시간(분) 보다 큰 경우.

4. minutes는 소요 시간(분)을 저장할 변수로, 2로 초기화한다.

5. grid의 모든 값을 순차적으로 아래를 검증한다.
- 하나라도 신선한 오렌지가 존재하면, -1을 주어진 문제의 결과로 반환한다.
- minutes에 minutes와 col 중 큰 값을 저장한다.

6. 반복이 완료되면 minutes에서 초기값인 2를 뺀 값을 주어진 문제의 결과로 반환한다.

# 해설
- minutes를 2로 초기화 하여 계산하는 이유는 썩은 오렌지의 위치에서 시간 계산을 수행할 때, 현재 값 이상으로 적용해야 별도의 배열을 생성하지 않고 grid를 이용하여 내 신선한 오렌지와 빈 칸의 값을 유지하며 시간을 누적 계산 할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RottingOranges.java){:target="_blank"}에서 확인 가능합니다.