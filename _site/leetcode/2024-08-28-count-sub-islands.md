---
title: "Leetcode Java Count Sub Islands"
excerpt: "Leetcode Count Sub Islands Java"
last_modified_at: 2024-08-28T18:50:00
header:
  image: /assets/images/leetcode/count-sub-islands.png
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
[Link](https://leetcode.com/problems/count-sub-islands/){:target="_blank"}

# 코드
```java
class Solution {

  public int countSubIslands(int[][] grid1, int[][] grid2) {
    int result = 0;
    for (int i = 0; i < grid2.length; i++) {
      for (int j = 0; j < grid2[0].length; j++) {
        if (grid2[i][j] == 1 && this.dfs(grid1, grid2, i, j)) {
          result++;
        }
      }
    }
    return result;
  }

  private boolean dfs(int[][] grid1, int[][] grid2, int i, int j) {
    boolean result = true;
    if (0 <= i && i < grid2.length && 0 <= j && j < grid2[0].length && grid2[i][j] == 1) {
      if (grid1[i][j] != grid2[i][j]) {
        result = false;
      }
      grid2[i][j] = 0;
      result &= this.dfs(grid1, grid2, i - 1, j);
      result &= this.dfs(grid1, grid2, i + 1, j);
      result &= this.dfs(grid1, grid2, i, j - 1);
      result &= this.dfs(grid1, grid2, i, j + 1);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/path-with-maximum-probability/submissions/1369877894/){:target="_blank"}

# 설명
1. 0은 물, 1은 땅을 나타내는 값을 가진 grid2의 육지가 grid1의 육지와 완전히 겹쳐지는 육지의 갯수를 저장하는 문제이다.

2. result는 grid2의 육지가 grid1의 육지와 완전히 겹처지는 육지의 갯수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 grid2 행의 길이 미만까지 i를, 0부터 grid2 열의 길이 미만까지 j를 증가시키며 아래를 수행한다.
- grid2[i][j]가 1이면서 4번에서 정의한 dfs(int[][] grid1, int[][] grid2, int i, int j) 메서드를 수행한 결과가 참인 경우, result를 증가시킨다.

4. DFS 방식으로 육지를 탐색할 dfs(int[][] grid1, int[][] grid2, int i, int j) 메서드를 정의한다.
- result는 grid2의 육지가 grid1의 육지와 겹쳐지는지 검증하기 위한 변수로, true로 초기화한다.
- i와 j가 grid2 범위 내 있으면서 grid2[i][j]의 값이 1인 육지인 경우, 아래를 수행한다.
  - grid1[i][j]의 값과 grid2[i][j]의 값이 동일하지 않으면 겹쳐지는 육지가 아니므로, result에 false를 넣어준다.
  - grid2[i][j]에 0을 넣어 이미 탐색한 위치임을 표시해준다.
  - result에 현재 위치에서 상하좌우로 재귀 호출한 결과를 순차적으로 AND(&) 비트 연산을 수행한 결과를 넣어준다.
- 수행이 완료되면 result를 반환한다.

5. 반복이 완료되어 조건을 만족하는 육지의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountSubIslands.java){:target="_blank"}에서 확인 가능합니다.