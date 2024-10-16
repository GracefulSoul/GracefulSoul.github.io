---
title: "Leetcode Java Game of Life"
excerpt: "Leetcode Game of Life Java 풀이"
last_modified_at: 2021-12-07T21:00:00
header:
  image: /assets/images/leetcode/game-of-life.png
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
[Link](https://leetcode.com/problems/game-of-life/){:target="_blank"}

# 코드
```java
class Solution {

  public void gameOfLife(int[][] board) {
    int rowSize = board.length;
    int colSize = board[0].length;
    for (int i = 0; i < rowSize; i++) {
      for (int j = 0; j < colSize; j++) {
        int lives = this.getLiveNeighbors(board, rowSize, colSize, i, j);
        if (board[i][j] == 1 && lives >= 2 && lives <= 3) {
          board[i][j] = 3;
        }
        if (board[i][j] == 0 && lives == 3) {
          board[i][j] = 2;
        }
      }
    }
    for (int i = 0; i < rowSize; i++) {
      for (int j = 0; j < colSize; j++) {
        board[i][j] >>= 1;
      }
    }
  }

  private int getLiveNeighbors(int[][] board, int m, int n, int i, int j) {
    int lives = 0;
    for (int x = Math.max(i - 1, 0); x <= Math.min(i + 1, m - 1); x++) {
      for (int y = Math.max(j - 1, 0); y <= Math.min(j + 1, n - 1); y++) {
        lives += board[x][y] & 1;
      }
    }
    lives -= board[i][j] & 1;
    return lives;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/598303826/){:target="_blank"}

# 설명
1. 주어진 2차원 정수 배열인 board를 이용하여 1970년 영국 수학자 Jone Horton Conway가 고안한 [Conway's Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life){:target="_blank"}를 수행하는 문제이다.
- 살아있는 세포는 1, 죽은 세포는 0으로 표시한다.
- 상, 하, 좌, 우, 대각의 총 8개 셀은 살아있는 이웃으로 판단한다.
- 아래 4개의 규칙에 의해 게임이 수행된다.
  - 살아있는 이웃이 2개 미만인 살아있는 세포는 죽게된다.
  - 2 ~ 3개의 살아있는 이웃이 있는 살아있는 세포는 그대로 살아있는다.
  - 살아있는 이웃이 3개인 죽은 세포는 살아난다.
  - 3개 초과의 살아있는 이웃이 있는 살아있는 세포는 죽게된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- rowSize는 board의 가로 길이인 board.length의 값을 저장하는 변수이다.
- colSize는 board의 세로 길이인 board[0].length의 값을 저장하는 변수이다.

3. board를 순차적으로 반복하기 전에, 살아있는 세포의 수를 검증하기 위한 getLiveNeighbors 메서드를 정의한다.
- 살아있는 세포의 수를 저장하기 위한 lives 변수를 정의한다.
- 살아있는 세포의 이웃에 대한 가로 축의 범위인 x는 $i - 1$과 0 중 큰 값부터 시작하여 $i + 1$과 $m - 1$ 중 작은 값까지 점층적으로 증가시키며 반복한다.
- 살아있는 세포의 이웃에 대한 세로 축의 범위인 y는 $j - 1$과 0 중 큰 값부터 시작하여 $j + 1$과 $n - 1$ 중 작은 값까지 점층적으로 증가시키며 반복한다.
  - boards[x][y]와 i의 AND(&) 비트 연산의 결과를 lives에 더하여 lives를 증가시킨다.
- 마지막으로 lives에 board[i][j]의 AND(&) 비트 연산의 결과를 lives에 빼서 lives를 감소시킨 값을 반환한다.

4. 3번을 이용하여 살아있는 세포의 수를 저장한 lives를 이용하여 아래를 수행한다.
- board[i][j]의 값이 1이고 lives가 2 혹은 3인 경우, board[i][j]에 3을 넣어준다.
  - 01(1)의 비트 값인 board[i][j] 값을 11(3)으로 만들어 넣는 이유는 3번의 비트 연산 수행에 &연산에 수행되는 값이 1과 같이 처리되기 위함이다.
  - 01(1) & 00(0) == 11(3) & 00(0) == 0와 01(1) & 01(1) == 11(3) & 01(1) == 1으로 이웃을 판단하는 로직에서는 동일 수행 결과를 만들어주고, 이후 살아있는 상태임을 표기하기 위함이다.
- board[i][j]의 값이 0이고 lives가 3인 경우, board[i][j]에 2를 넣어준다.
  - 00(0)의 비트 값인 board[i][j] 값을 10(2)으로 만들어 넣는 이유는 3번의 비트 연산 수행에 &연산에 수행되는 값이 0과 같이 처리되기 위함이다.
  - 00(0) & 00(0) == 10(2) & 00(0) == 00(0) & 01(1) == 10(2) & 01(1) == 0으로 이웃을 판단하는 로직에서는 동일 수행 결과를 만들어주고, 이후 살아있는 상태임을 표기하기 위함이다.

5. 4번을 통해서 board에 넣어준 2(<b>1</b>1)와 3(<b>1</b>0)의 값들의 두 번째 비트 값을 board에 다시 넣어, 2와 3이 들어간 값은 살아있는 세포로 표기해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GameOfLife.java){:target="_blank"}에서 확인 가능합니다.