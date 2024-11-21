---
title: "Leetcode Java Count Unguarded Cells in the Grid"
excerpt: "Leetcode - 'Count Unguarded Cells in the Grid' 문제 Java 풀이"
last_modified_at: 2024-11-21T18:40:00
header:
  image: /assets/images/leetcode/count-unguarded-cells-in-the-grid.png
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
[Link](https://leetcode.com/problems/count-unguarded-cells-in-the-grid/){:target="_blank"}

# 코드
```java
class Solution {

  public int countUnguarded(int m, int n, int[][] guards, int[][] walls) {
    int[][] grid = new int[m][n];
    for (int[] wall : walls) {
      grid[wall[0]][wall[1]] = 1;
    }
    for (int[] guard : guards) {
      grid[guard[0]][guard[1]] = 1;
    }
    int count = (m * n) - guards.length - walls.length;
    for (int[] guard : guards) {
      int x = guard[0] - 1;
      int y = guard[1];
      while (x >= 0 && grid[x][y] != 1) {
        if (grid[x][y] != -1) {
          count--;
          grid[x][y] = -1;
        }
        x--;
      }
      x = guard[0] + 1;
      while (x < m && grid[x][y] != 1) {
        if (grid[x][y] != -1) {
          count--;
          grid[x][y] = -1;
        }
        x++;
      }
      x = guard[0];
      y = guard[1] - 1;
      while (y >= 0 && grid[x][y] != 1) {
        if (grid[x][y] != -1) {
          count--;
          grid[x][y] = -1;
        }
        y--;
      }
      y = guard[1] + 1;
      while (y < n && grid[x][y] != 1) {
        if (grid[x][y] != -1) {
          count--;
          grid[x][y] = -1;
        }
        y++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-unguarded-cells-in-the-grid/submissions/1459078417/){:target="_blank"}

# 설명
1. $n \times m$ 크기의 2차원 배열에서 경비원의 좌표가 저장된 guards를 이용하여 벽의 좌표가 저장된 walls 중 하나 혹은 배열의 끝에 다다를 때 까지 이동 가능할 때 마주치지 않을 수 있는 공간의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- grid는 경비원을 마주치지 않을 수 있는 공간을 계산하기 위한 변수로, $n \times m$ 크기의 2차원 배열로 초기화하고 walls와 guards의 위치에 1을 넣어준다.
- count는 경비원을 마주치지 않을 수 있는 공간의 수를 저장할 변수로, 위의 값을 제외한 빈 공간의 갯수로 초기화한다.

3. guards를 순차적으로 guard에 넣어 아래를 수행한다.
- x와 y는 좌표를 저장할 변수로, 경비원의 좌측인 $guard[0] - 1$과 guard[1]의 값으로 초기화한다.
- x가 0 이상이면서 grid[x][y]가 1이 아닌 이동 불가능한 위치가 아닐 때 까지 아래를 수행한다.
  - grid[x][y]의 값이 -1이 아닌 이동한 경로가 아닌 경우, count를 감소시키고 grid[x][y]에 -1을 넣어 이동한 위치임을 표시한다.
  - x를 감소시켜 좌측으로 이동한다.
- x에 $gurad[0] + 1$을 넣어, 경비원의 오른쪽 위치로 이동한다.
- x가 m 미만이면서 grid[x][y]가 1이 아닌 이동 불가능한 위치가 아닐 때 까지 아래를 수행한다.
  - grid[x][y]의 값이 -1이 아닌 이동한 경로가 아닌 경우, count를 감소시키고 grid[x][y]에 -1을 넣어 이동한 위치임을 표시한다.
  - x를 증가시켜 우측으로 이동한다.
- x에 guard[0]를, y에 $guard[1] - 1$를 넣어, 경비원의 아래 위치로 이동한다.
  - grid[x][y]의 값이 -1이 아닌 이동한 경로가 아닌 경우, count를 감소시키고 grid[x][y]에 -1을 넣어 이동한 위치임을 표시한다.
  - y를 감소시켜 아래로 이동한다.
- y에 $guard[1] + 1$을 넣어, 경비원의 위 위치로 이동한다.
  - grid[x][y]의 값이 -1이 아닌 이동한 경로가 아닌 경우, count를 감소시키고 grid[x][y]에 -1을 넣어 이동한 위치임을 표시한다.
  - y를 증가시켜 위로 이동한다.

4. 반복이 완료되면 계산된 마주치지 않는 공간의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountUnguardedCellsInTheGrid.java){:target="_blank"}에서 확인 가능합니다.