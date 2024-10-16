---
title: "Leetcode Java Minesweeper"
excerpt: "Leetcode Minesweeper Java"
last_modified_at: 2022-06-14T21:00:00
header:
  image: /assets/images/leetcode/minesweeper.png
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
[Link](https://leetcode.com/problems/minesweeper/){:target="_blank"}

# 코드
```java
class Solution {

  public char[][] updateBoard(char[][] board, int[] click) {
    int x = click[0];
    int y = click[1];
    if (board[x][y] == 'M') {
      board[x][y] = 'X';
    } else {
      this.dfs(board, x, y, board.length, board[0].length);
    }
    return board;
  }

  private void dfs(char[][] board, int x, int y, int rowLength, int colLength) {
    if (x < 0 || y < 0 || x >= rowLength || y >= colLength || board[x][y] != 'E') {
      return;
    }
    int num = this.findMines(board, x, y, rowLength, colLength);
    if (num == 0) {
      board[x][y] = 'B';
      for (int i = -1; i <= 1; i++) {
        for (int j = -1; j <= 1; j++) {
          this.dfs(board, x + i, y + j, rowLength, colLength);
        }
      }
    } else {
      board[x][y] = (char) ('0' + num);
    }
  }

  private int findMines(char[][] board, int x, int y, int rowLength, int colLength) {
    int count = 0;
    for (int i = -1; i <= 1; i++) {
      for (int j = -1; j <= 1; j++) {
        int x1 = x + i;
        int y1 = y + j;
        if (x1 >= 0 && y1 >= 0 && x1 < rowLength && y1 < colLength && board[x1][y1] == 'M') {
          count++;
        }
      }
    }
    return count;
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/722002583/){:target="_blank"}

# 설명
1. board 크기의 지뢰찾기 게임을 하는 중 click한 위치부터 시작해서 지뢰를 모두 찾을 때 까지 단계를 반복하여 board를 반환하는 문제이다.
- 'M'은 미공개 지뢰를 의미한다.
- 'E'는 드러나지 않은 셀을 의미한다.
- 'B'는 인접한 지뢰가 없는 빈 셀을 의미한다.
- 'X'는 드러난 지뢰를 의미한다.

2. 클릭한 위치가 지뢰인 경우 지뢰를 클릭했으므로, 해당 위치를 'X'로 변경하고 board를 반환한다.

3. 클릭한 위치가 지뢰가 아닌 경우, 4번에서 정의한 dfs(char[][] board, int x, int y, int rowLength, int colLength) 메서드를 수행한다.

4. DFS 방식으로 지뢰를 찾기 위한 dfs(char[][] board, int x, int y, int rowLength, int colLength) 메서드를 정의한다.
- x가 배열의 x축 범위를 벗어나거나, y가 y축 범위를 벗어나면 수행을 종료한다.
- num에 5번에서 인접한 지뢰의 개수를 찾기 위한 findMines(char[][] board, int x, int y, int rowLength, int colLength) 메서드를 수행한 결과를 반환한다.
- num이 0이면 지뢰가 없으므로, board[x][y]에 'B'를 넣어주고, x와 y 인접 셀을 재귀 호출을 이용하여 탐색한다.
- num이 0이 아니면 board[x][y]에 인접한 지뢰의 개수를 넣어준다.

5. 지뢰의 개수를 탐색하기 위한 findMines(char[][] board, int x, int y, int rowLength, int colLength) 메서드를 정의한다.
- 지뢰의 개수를 넣을 count를 0으로 정의한다.
- x와 y축을 1씩 가감하며 'M'의 개수를 찾아 count를 증가시키고 해당 값을 반환한다.

6. 4 ~ 5번의 수행이 완료되면 지뢰찾기 게임을 완성한 board를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Minesweeper.java){:target="_blank"}에서 확인 가능합니다.