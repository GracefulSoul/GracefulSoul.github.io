---
title: "Leetcode Java Surrounded Regions"
excerpt: "Leetcode - 'Surrounded Regions' 문제 Java 풀이"
last_modified_at: 2021-08-19T12:00:00
header:
  image: /assets/images/leetcode/surrounded-regions.png
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
[Link](https://leetcode.com/problems/surrounded-regions/){:target="_blank"}

# 코드
```java
class Solution {

  public void solve(char[][] board) {
    for (int i = 0; i < board.length; i++) {
      if (board[i][0] == 'O') {
        this.dfs(i, 1, board);
      }
      if (board[i][board[0].length - 1] == 'O') {
        this.dfs(i, board[0].length - 2, board);
      }
    }
    for (int i = 0; i < board[0].length; i++) {
      if (board[0][i] == 'O') {
        this.dfs(1, i, board);
      }
      if (board[board.length - 1][i] == 'O') {
        this.dfs(board.length - 2, i, board);
      }
    }
    for (int i = 1; i < board.length - 1; i++) {
      for (int j = 1; j < board[0].length - 1; j++) {
        if (board[i][j] == 'o') {
          board[i][j] = 'O';
        } else if (board[i][j] == 'O') {
          board[i][j] = 'X';
        }
      }
    }
  }

  private void dfs(int i, int j, char[][] board) {
    if (i == 0 || j == 0 || i == board.length - 1 || j == board[0].length - 1 || board[i][j] == 'X' || board[i][j] == 'o') {
      return;
    }
    if (board[i][j] == 'O') {
      board[i][j] = 'o';
    }
    this.dfs(i + 1, j, board);
    this.dfs(i - 1, j, board);
    this.dfs(i, j + 1, board);
    this.dfs(i, j - 1, board);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/540708633/){:target="_blank"}

# 설명
1. 주어진 'O'와 'X'의 값들로 차있는 2차원 배열 board를 이용하여 4방향이 'X'로 이루어진 'O'만 남기고 나머지를 'X'로 바꾸는 문제이다.

2. 0부터 행의 개수만큼 반복하여 외각의 값인 board[i][0]과 board[i][$board[0].legnth - 1$]의 값이 'O'인지 검증하여 그 옆의 값 위주로 검증하여 주변이 'X'인 'O'만 'o'로 변경하여 대상을 표시한다.

3. 0부터 열의 개수만큼 반복하여 외각의 값인 board[0][i]]과 board[$board.legnth - 1$][i]의 값이 'O'인지 검증하여 그 옆의 값 위주로 검증하여 주변이 'X'인 'O'만 'o'로 변경하여 대상을 표시한다.

4. 외각을 제외한 모든 행과 열을 반복하여 수정된 board를 이용하여 'o'인 값만 'O'로 변경해주고, 나머지는 'X'로 전부 바꾸어주어 문제를 해결한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SurroundedRegions.java){:target="_blank"}에서 확인 가능합니다.