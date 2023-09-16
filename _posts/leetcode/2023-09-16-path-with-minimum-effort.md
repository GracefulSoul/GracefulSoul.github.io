---
title: "Leetcode Java Path With Minimum Effort"
excerpt: "Leetcode Path With Minimum Effort Java"
last_modified_at: 2023-09-16T09:50:00
header:
  image: /assets/images/leetcode/path-with-minimum-effort.png
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
[Link](https://leetcode.com/problems/path-with-minimum-effort){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumEffortPath(int[][] heights) {
    int row = heights.length;
    int col = heights[0].length;
    Queue<int[]> queue = new PriorityQueue<>((a, b) -> a[2] - b[2]);
    int[][] dist = new int[row][col];
    int[][] directions = { { -1, 0 }, { 0, 1 }, { 1, 0 }, { 0, -1 } };
    for (int[] r : dist) {
      Arrays.fill(r, Integer.MAX_VALUE);
    }
    dist[0][0] = 0;
    queue.add(new int[] { 0, 0, 0 });
    while (!queue.isEmpty()) {
      int[] curr = queue.poll();
      int x = curr[0];
      int y = curr[1];
      int diff = curr[2];
      if (x == row - 1 && y == col - 1) {
        return diff;
      }
      for (int[] direction : directions) {
        int nx = x + direction[0];
        int ny = y + direction[1];
        if (nx >= 0 && nx < row && ny >= 0 && ny < col) {
          int next = Math.max(diff, Math.abs(heights[nx][ny] - heights[x][y]));
          if (next < dist[nx][ny]) {
            dist[nx][ny] = next;
            queue.add(new int[] { nx, ny, next });
          }
        }
      }
    }
    return 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/path-with-minimum-effort/submissions/1050506436/){:target="_blank"}

# 설명
1. heights의 좌측 상단부터 우측 하단까지 이동하기 위한 최소한의 노력을 구하는 문제이다.
- 최소한의 노력은 이동하는 셀의 절대적 값의 차이이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 height의 행과 열의 길이를 저장한 변수이다.
- queue는 높이 차이를 오름차순으로 저장하여 관리할 변수로, PriorityQueue로 각 값의 세 번째 값의 차이의 오름차순으로 정렬되도록 초기화하고 첫 값을 [0, 0, 0]으로 넣어준다.
- dist는 이동에 대한 절대적 값의 차이를 저장할 변수로, $row \times col$ 크기의 배열로 초기화하고 모든 값을 Integer의 최댓 값으로 넣어준다.
- directions는 이동 방향을 저장할 변수로, 좌우상하 순의 [x, y] 좌표를 넣어준다.

3. queue가 비어있지 않을 때까지 아래를 반복한다.
- curr에 queue의 앞에 있는 값을 꺼내 넣어준 후 x, y, diff에 순차적으로 값을 넣어준다.
- 현재 위치가 우측 하단의 마지막 위치인 경우, diff을 주어진 문제의 결과로 반환한다.
- directions를 direction에 순차적으로 넣고 아래를 반복한다.
  - nx에 x와 direction[0]을 더해서, ny에 y와 direction[1]을 더해서 넣어준다.
  - nx가 [0, row] 범위에 존재하면서 ny가 [0, col] 범위에 존재하는 경우, 아래를 계속 수행하고 아니면 다음 반복을 수행한다.
  - next에 diff와 heights[nx][ny]의 값과 heights[x][y]의 차잇값 중 큰 값을 넣어준다.
  - next가 dist[nx][ny]의 값보다 작은 경우, dist[nx][ny]에 next를 넣어주고 queue에 [nx, ny, next]를 넣어준다.

4. 반복이 완료되면 최소한의 노력으로 이동할 수 없으므로, 0을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PathWithMinimumEffort.java){:target="_blank"}에서 확인 가능합니다.