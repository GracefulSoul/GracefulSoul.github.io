---
title: "Leetcode Java Cut Off Trees for Golf Event"
excerpt: "Leetcode - 'Cut Off Trees for Golf Event' 문제 Java 풀이"
last_modified_at: 2022-09-28T19:50:00
header:
  image: /assets/images/leetcode/cut-off-trees-for-golf-event.png
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
[Link](https://leetcode.com/problems/cut-off-trees-for-golf-event){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[][] DIRECTIONS = {
    { 0, 1 },
    { 1, 0 },
    { 0, -1 },
    { -1, 0 }
  };
  
  public int cutOffTree(List<List<Integer>> forest) {
    int row = forest.size();
    int col = forest.get(0).size();
    List<int[]> trees = new ArrayList<>();
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (forest.get(i).get(j) > 1) {
          trees.add(new int[] { i, j, forest.get(i).get(j) });
        }
      }
    }
    Collections.sort(trees, (tree1, tree2) -> tree1[2] - tree2[2]);
    int result = 0;
    int x = 0;
    int y = 0;
    for (int[] tree : trees) {
      int steps = this.bfs(forest, row, col, x, y, tree);
      if (steps < 0) {
        return -1;
      }
      result += steps;
      x = tree[0];
      y = tree[1];
    }
    return result;
  }

  private int bfs(List<List<Integer>> forest, int row, int col, int x, int y, int[] tree) {
    Queue<int[]> queue = new LinkedList<>();
    queue.add(new int[] { x, y });
    boolean[][] visited = new boolean[row][col];
    visited[x][y] = true;
    int steps = 0;
    while (!queue.isEmpty()) {
      int size = queue.size();
      while (size-- > 0) {
        int[] curr = queue.poll();
        if (curr[0] == tree[0] && curr[1] == tree[1]) {
          return steps;
        }
        for (int[] direction : DIRECTIONS) {
          x = direction[0] + curr[0];
          y = direction[1] + curr[1];
          if (x < 0 || y < 0 || x >= row || y >= col || visited[x][y] || forest.get(x).get(y) == 0) {
            continue;
          }
          visited[x][y] = true;
          queue.add(new int[] { x, y });
        }
      }
      steps++;
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/809708790/){:target="_blank"}

# 설명
1. 2차원 숲의 지도를 나타내는 forest를 이용하여 아래의 규칙대로 모든 나무를 자를 수 있는 최소 단계를 구하는 문제이다.
- forest의 값은 각각 아래의 의미를 가진다.
  - 0은 통과할 수 없는 길을 나타낸다.
  - 1은 걸어서 통과할 수 있는 길을 나타낸다.
  - 1보다 큰 값은 나무의 높이를 나타낸다.
- 첫 위치인 (0, 0)에서 동서남북 모든 방향으로 이동이 가능하며, 나무를 마주치면 자를 수 있다.
- 나무를 자르는 순서는 낮은 순에서 높은 순으로 잘라야 하며, 자른 나무의 위치 값은 길(forest의 값인 1)이 된다.
- 모든 나무를 자를 수 없으면 -1을 반환한다.
- 동일한 높이의 나무는 없으며, 최소한 하나 이상의 나무를 자를 수 있는 입력 값(forest)이 주어진다.

2. 한 위치에서 동서남북 모든 방향을 구할 수 있는 전역 변수인 DIRECTIONS를 정의하고, 현재 위치 기준으로 위, 왼쪽, 아래, 오른쪽의 위치를 임의 순서로 넣어준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 forest의 행과 열의 길이를 저장한 변수이다.
- trees는 나무 위치를 새로 저장할 변수로, ArrayList로 초기화하고 forest 내 값이 0이 아닌 모든 나무의 정보를 [행 위치, 열 위치, 높이] 형태의 배열로 넣어준다.

4. trees의 모든 값들을 높이 기준으로 오름차순 정렬한다.

5. 모든 나무를 자르기 위한 최소 이동 횟수인 result와 행과 열 위치를 임시 저장할 x와 y 모두 0으로 초기화한다.

6. trees의 모든 tree를 이용하여 아래를 반복한다.
- steps에 7번에서 정의한 bfs(List<List<Integer>> forest, int row, int col, int x, int y, int[] tree)를 이용하여 최소 이동 횟수를 구해준다.
- steps가 0 미만인 경우 나무를 자르기 위해 이동할 수 없으므로, -1을 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니라면 result에 steps를 더해주고, x와 y에 tree의 첫 번째와 두 번째인 행과 열의 위치를 넣어주고 반복을 계속 수행한다.

7. x와 y의 위치에서 다음으로 잘라야 하는 나무의 위치인 tree까지 최소 이동 횟수를 계산하기 위한 bfs(List<List<Integer>> forest, int row, int col, int x, int y, int[] tree) 메서드를 정의한다.
- 메서드를 수행하기 위한 변수를 정의한다.
  - queue는 자를 수 있는 나무를 임시 저장하기 위한 변수로, LinkedList로 초기화하고 현재 위치인 x와 y를 배열로 넣어준다.
  - visited는 이동 위치를 저장하기 위한 배열로, $row \times col$ 크기의 2차원 배열로 정의하고 초기 위치인 visited[x][y]를 true로 초기화한다.
  - steps는 tree까지 이동하기 위한 이동 거리를 저장할 변수로, 0으로 초기화한다.
- queue가 비어있지 않을 때 까지 반복하고, size에 queue의 크기를 넣은 후 size가 0이 될 때 까지 아래를 반복한다.
  - curr에 queue에서 꺼낸 나무의 위치를 넣어준다.
  - 만일 tree의 위치와 curr이 동일한 경우, [x, y]에서 출발하여 tree에 도착하기위한 최소 이동 거리인 steps를 반환한다.
  - 위의 경우가 아니라면 DIRECTIONS를 반복하여 [x, y] 위치의 동서남북 위치의 나무가 존재하면 x축과 y축을 배열로 생성하여 queue 넣어주고 visited의 각 위치를 true로 변경해준다.
- 위의 반복이 완료되면 steps를 증가시키고, 다시 queue가 비어있지 않을 때 까지 반복을 수행한다.
- queue가 빌때 까지 반복이 완료되면 tree에 도달하지 못하였으므로, -1을 반환한다.

8. 6번의 반복이 완료되면 최소 이동 거리를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CutOffTreesForGolfEvent.java){:target="_blank"}에서 확인 가능합니다.