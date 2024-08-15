---
title: "Leetcode Java As Far from Land as Possible"
excerpt: "Leetcode As Far from Land as Possible Java"
last_modified_at: 2024-08-15T21:50:00
header:
  image: /assets/images/leetcode/as-far-from-land-as-possible.png
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
[Link](https://leetcode.com/problems/as-far-from-land-as-possible/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[][] DIRECTIONS = {
    { 0, 1 },
    { 0, -1 },
    { 1, 0 },
    { -1, 0 }
  };

  public int maxDistance(int[][] grid) {
    int length = grid.length;
    Queue<int[]> queue = new LinkedList<>();
    for (int i = 0; i < length; i++) {
      for (int j = 0; j < length; j++) {
        if (grid[i][j] == 1) {
          queue.offer(new int[] { i, j });
        }
      }
    }
    int result = -1;
    if (!queue.isEmpty() && queue.size() != length * length) {
      while (!queue.isEmpty()) {
        int size = queue.size();
        result++;
        while (size-- > 0) {
          int[] point = queue.poll();
          int x = point[0];
          int y = point[1];
          for (int[] direction : DIRECTIONS) {
            int nx = x + direction[0];
            int ny = y + direction[1];
            if (nx >= 0 && nx < length && ny >= 0 && ny < length && grid[nx][ny] == 0) {
              grid[nx][ny] = 1;
              queue.offer(new int[] { nx, ny });
            }
          }
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/as-far-from-land-as-possible/submissions/1356558984/){:target="_blank"}

# 설명
1. 0인 물과 1인 육지로 이루어진 정사각형의 grid를 이용하여 각 육지에서 최대 거리가 되는 위치를 구하여 육지별 최대 거리를 반환하는 문제이다.
- 위의 거리는 [Manhattan distance](https://en.wikipedia.org/wiki/Taxicab_geometry){:target="_blank"}를 의미하며, 해당 거리는 (x0, y0)과 (x1, y1) 두 지점에 대해서 $|x0 - x1| + |y0 - y1|$로 측정된다.
- 해당 조건을 만족하는 위치가 존재하지 않으면 -1을 주어진 문제의 결과로 반환한다.

2. 전역 변수인 DIRECTIONS는 상하좌우를 탐색하기 위한 변수로 현재 위치에서 이동하는 x와 y축의 네 쌍을 저장한 변수이다.

3. 문제 풀이에 필요한 변수를 정의한다.
- length는 grid의 길이를 저장한 변수로, 정사각형이므로 하나의 길이만 저장한다.
- queue는 육지의 각 위치를 저장할 변수로, grid에서 육지에 해당 하는 위치를 queue에 (x, y) 형태의 2차원 정수 배열로 넣어준다.
- result는 육지별 최대 거리를 저장할 변수로, 위치가 존재하지 않는 경우의 결과인 -1로 초기화한다.

4. queue가 비어있지 않거나 grid가 모두 육지로 되어있지 않은 경우, queue가 비어있지 않을 때 까지 아래를 반복한다.
- size에 현재 queue의 크기를 넣어준다.
- result를 증가하여 이동하는 거리를 증가시킨 후, size가 0보다 클 때 까지 아래를 반복하고 size를 감소시켜준다.
  - point에 queue의 첫 값을 넣은 후 x와 y에 각 위치를 넣어준다.
  - DIRECTIONS를 순차적으로 direction에 넣어 x와 y에 더한 후, grid 범위 내 물의 위치이면 해당 값을 1을 넣어 육지로 변환 후 다음 탐색의 경우의 수인 해당 위치를 queue에 넣어준다.

5. 반복이 완료되면 최대 거리가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AsFarFromLandAsPossible.java){:target="_blank"}에서 확인 가능합니다.