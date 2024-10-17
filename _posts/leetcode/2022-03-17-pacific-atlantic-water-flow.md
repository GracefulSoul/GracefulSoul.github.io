---
title: "Leetcode Java Pacific Atlantic Water Flow"
excerpt: "Leetcode - 'Pacific Atlantic Water Flow' 문제 Java 풀이"
last_modified_at: 2022-03-17T12:00:00
header:
  image: /assets/images/leetcode/pacific-atlantic-water-flow.png
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
[Link](https://leetcode.com/problems/pacific-atlantic-water-flow/){:target="_blank"}

# 코드
```java
class Solution {

  private List<List<Integer>> result;
  private boolean[][] pacific;
  private boolean[][] atlantic;

  public List<List<Integer>> pacificAtlantic(int[][] heights) {
    int row = heights.length;
    int col = heights[0].length;
    this.result = new ArrayList<>();
    this.pacific = new boolean[row][col];
    this.atlantic = new boolean[row][col];
    for (int idx = 0; idx < row; idx++) {
      this.dfs(heights, this.pacific, idx, 0, row, col);
      this.dfs(heights, this.atlantic, idx, col - 1, row, col);
    }
    for (int idx = 0; idx < col; idx++) {
      this.dfs(heights, this.pacific, 0, idx, row, col);
      this.dfs(heights, this.atlantic, row - 1, idx, row, col);
    }
    return this.result;
  }

  private void dfs(int[][] heights, boolean[][] visit, int i, int j, int row, int col) {
    if (visit[i][j]) {
      return;
    }
    visit[i][j] = true;
    if (this.pacific[i][j] && this.atlantic[i][j]) {
      List<Integer> temp = new ArrayList<>();
      temp.add(i);
      temp.add(j);
      this.result.add(temp);
    }
    if (i + 1 < row && heights[i + 1][j] >= heights[i][j]) {
      this.dfs(heights, visit, i + 1, j, row, col);
    }
    if (i - 1 >= 0 && heights[i - 1][j] >= heights[i][j]) {
      this.dfs(heights, visit, i - 1, j, row, col);
    }
    if (j + 1 < col && heights[i][j + 1] >= heights[i][j]) {
      this.dfs(heights, visit, i, j + 1, row, col);
    }
    if (j - 1 >= 0 && heights[i][j - 1] >= heights[i][j]) {
      this.dfs(heights, visit, i, j - 1, row, col);
    }
    return;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/661540164/){:target="_blank"}

# 설명
1. Pacific과 Atlantic 해안을 인접하고 있는 섬의 높이를 나타내는 heights가 주어지면, 빗물이 올 경우 두 해안으로 흐를 수 있는 경계가 되는 구간을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row는 heights 배열 내 행의 개수를 저장할 변수로, heights의 행의 개수로 초기화한다.
- col은 heights 배열 내 열의 개수를 저장할 변수로, heights의 첫 행의 열 개수로 초기화한다.
- result는 결과를 저장할 List로, 새 ArrayList로 정의한다.
- pacific은 Pacific 해안으로 빗물이 흐를 가능성이 있는지 저장할 배열로, heights와 동일한 크기로 초기화한다.
- atlantic은 Atlantic 해안으로 빗물이 흐를 가능성이 있는지 저장할 배열로, heights와 동일한 크기로 초기화한다.

3. 0부터 row의 크기 전까지 증가시키며 5번에서 정의한 dfs(int[][] heights, boolean[][] visit, int i, int j, int row, int col) 메서드를 pacific은 (idx, j)로 atlantic은 (idx, $col - 1$)로 수행한다.

4. 0부터 col의 크기 전까지 증가시키며 5번에서 정의한 dfs(int[][] heights, boolean[][] visit, int i, int j, int row, int col) 메서드를 pacific은 (0, idx)로 atlantic은 ($row - 1$, idx)로 수행한다.

5. DFS 방식으로 문제를 해결할 dfs(int[][] heights, boolean[][] visit, int i, int j, int row, int col) 메서드를 정의한다.
- visit[i][j]가 true인 경우 이전에 수행된 위치이므로, 수행을 그만한다.
- visit[i][j]에 true를 넣어 수행 여부를 체크해둔다.
- pacific[i][j]의 값이 true이고 atlantic[i][j]의 값이 true인 경우 양 해안가로 빗물이 흐를 수 있으므로, i와 j를 새 ArrayList에 넣어 result에 추가한다.
- $i + 1$이 row보다 작고 heights[$i + 1$][j]의 값이 heights[i][j]의 값보다 크거나 같은 경우, i를 증가시키고 dfs 메서드를 수행하여 배열의 위에서 아래로 가장 높은 지역을 탐색한다.
- $i - 1$이 0보다 크고 heights[$i - 1$][j]의 값이 heights[i][j]의 값보다 크거나 같은 경우, i를 감소시키고 dfs 메서드를 수행하여 배열의 아래에서 위로 가장 높은 지역을 탐색한다.
- $j + 1$이 col보다 작고 heights[i][$j + 1$]의 값이 heights[i][j]의 값보다 크거나 같은 경우, j를 증가시키고 dfs 메서드를 수행하여 배열의 좌측에서 우측으로 가장 높은 지역을 탐색한다.
- $j - 1$이 0보다 크고 heights[i][$j - 1$]의 값이 heights[i][j]의 값보다 크거나 같은 경우, j를 감소시키고 dfs 메서드를 수행하여 배열의 우측에서 좌측으로 가장 높은 지역을 탐색한다.

6. 반복이 완료하여 result에 경계의 위치 값을 다 넣었으면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PacificAtlanticWaterFlow.java){:target="_blank"}에서 확인 가능합니다.