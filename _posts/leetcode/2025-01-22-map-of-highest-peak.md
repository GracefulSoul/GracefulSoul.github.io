---
title: "Leetcode Java Map of Highest Peak"
excerpt: "Leetcode - 'Map of Highest Peak' 문제 Java 풀이"
last_modified_at: 2025-01-22T19:10:00
header:
  image: /assets/images/leetcode/map-of-highest-peak.png
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
[Link](https://leetcode.com/problems/map-of-highest-peak/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[] DIRECTIONS = { 0, 1, 0, -1, 0 };

  public int[][] highestPeak(int[][] isWater) {
    int row = isWater.length;
    int col = isWater[0].length;
    int[][] heights = new int[row][col];
    Queue<int[]> queue = new LinkedList<>();
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (isWater[i][j] == 1) {
          heights[i][j] = 0;
          queue.offer(new int[] { i, j });
        } else {
          heights[i][j] = -1;
        }
      }
    }
    while (!queue.isEmpty()) {
      int[] curr = queue.poll();
      for (int k = 0; k < 4; k++) {
        int x = curr[0] + DIRECTIONS[k];
        int y = curr[1] + DIRECTIONS[k + 1];
        if (0 <= x && x < row && 0 <= y && y < col && heights[x][y] < 0) {
          heights[x][y] = heights[curr[0]][curr[1]] + 1;
          queue.offer(new int[] { x, y });
        }
      }
    }
    return heights;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/map-of-highest-peak/submissions/1516732531/){:target="_blank"}

# 설명
1. 물의 위치를 1로 표시한 $m \times n$ 크기의 배열인 isWater를 이용하여 아래의 규칙을 만족하는 높이가 저장된 배열을 만들어 반환하는 문제이다.
- 물로 표시된 높이는 0으로 표시하고, 해당 상하좌우 셀의 값은 물보다 높으므로 1로 표시한다.
- 땅과 근접한 셀과의 높이 차이는 최대 1이어야한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- DIRECTIONS는 인접한 두 값의 조합이 상하좌우를 모두 표시할 수 있는 값의 조합을 저장한 전역 변수이다.
- row와 col은 isWater의 행과 열의 갯수를 저장한 변수이다.
- heights는 규칙을 만족하는 높이를 계산하여 저장할 배열로, isWater과 동일한 $row \times col$ 크기의 2차원 정수 배열로 정의한다.
- queue는 물의 위치를 저장하여 해당 위치부터 순차적인 높이를 계산하기 위한 변수로, LinkedList로 초기화한다.

3. 0 부터 row 미만까지 i를, 0 부터 col 미만까지 j를 순차적으로 증가시키며 아래를 반복한다.
- isWater[i][j]의 값이 1인 물인 경우, heights[i][j]의 위치에 0을 넣어주고 queue에 해당 위치를 배열로 넣어준다.
- isWater[i][j]의 값이 0인 땅인 경우, heights[i][j]의 위치에 -1을 넣어준다.

4. queue가 비어있지 않을 때 까지 아래를 반복하여 heights를 완성한다.
- curr에 queue의 맨 앞 값을 꺼내 넣어준다.
- 0부터 4미만까지 k를 증가시키며 아래를 반복한다.
  - x에 $curr[0] + DIRECTIONS[k]$ 값을, y에 $curr[1] + DIRECTIONS[k + 1]$ 값을 저장하여 다음 위치로 이동한다.
  - heights[x][y]의 값이 배열 범위 내이면서 값이 -1인 높이가 계산되지 않은 육지인 경우, 해당 위치에 이전 위치보다 1 큰 값을 넣고 queue에 [x, y] 좌표의 값을 배열로 넣어 물에서 현재 떨어진 위치 상하좌우 반복 이후 다음 위치 탐색 대상으로 저장한다.

5. 반복이 완료되어 완성된 높이가 저장된 heights를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MapOfHighestPeak.java){:target="_blank"}에서 확인 가능합니다.