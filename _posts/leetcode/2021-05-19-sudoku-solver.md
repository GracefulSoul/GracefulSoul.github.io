---
title: "Leetcode Java Sudoku Solver"
excerpt: "Leetcode - 'Sudoku Solver' 문제 Java 풀이"
last_modified_at: 2021-05-19T11:40:00
header:
  image: /assets/images/leetcode/find-first-and-last-position-of-element-in-sorted-array.png
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
[Link](https://leetcode.com/problems/sudoku-solver/){:target="_blank"}

# 코드
```java
class Solution {

  public void solveSudoku(char[][] board) {
    if (board == null || board.length == 0) {
      return;
    }
    this.solve(board);
  }

  private boolean solve(char[][] board) {
    for (int i = 0; i < board.length; i++) {
      for (int j = 0; j < board[i].length; j++) {
        if (board[i][j] == '.') {
          for (char c = '1'; c <= '9'; c++) {
            if (this.isValid(board, i, j, c)) {
              board[i][j] = c;
              if (this.solve(board)) {
                return true;
              } else {
                board[i][j] = '.';
              }
            }
          }
          return false;
        }
      }
    }
    return true;
  }

  private boolean isValid(char[][] board, int row, int col, char c) {
    for (int i = 0; i < 9; i++) {
      if (board[i][col] != '.' && board[i][col] == c ||
        board[row][i] != '.' && board[row][i] == c ||
        (
          board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] != '.' &&
          board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] == c
        )
      ) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/495130327/){:target="_blank"}

# 설명
1. 이전의 [Valid Sudoku](../valid-sudoku) 문제와 유사하게 기본 조건은 아래와 같이 동일하며, 주어진 변수 board에 완벽한 스도쿠 판을 채우는 문제이다.
- 주어진 스도쿠의 크기는 $9 \times 9$의 크기로 숫자는 1 ~ 9 까지 존재한다.
- 각 가로열에는 1 ~ 9 까지의 숫자가 고유하게 들어가야 한다.
- 각 세로열에는 1 ~ 9 까지의 숫자가 고유하게 들어가야 한다.
- $3 \times 3$ 크기로 나눈 9개의 정육면체 배열에 1 ~ 9 까지 숫자가 고유하게 들어가야 한다.

2. 반복을 통해 i는 row, j는 col 영역을 순환하며 '.' 문자가 존재하는 경우만 1 ~ 9 까지 숫자가 들어갈 수 있는지를 검증한다.

3. 다시 변수 c를 '1' ~ '9'의 문자를 반복하여 들어갈 수 있는지를 1번의 기본 조건을 만족하는지 검증한다.
- 조건을 만족하는 경우 true를 반환하고, 만족하지 않는 경우 false를 반환한다.
- 만일 만족하지 않는 경우는 무시하고 다음 숫자로 다시 검색한다.

4. 기본 조건을 만족하는 경우, 해당 위치에 문자를 주입하고, 다시 재귀 호출을 사용하여 처음부터 검증을 다시 수행한다.
- 재귀 호출의 결과가 true인 경우, 스도쿠 문자열의 배열이 정상적으로 끝난 경우이므로 true를 반환한다.
- 재귀 호출의 결과가 false인 경우, 해당 자리에 들어갈 숫자가 아니므로 board[i][j] 자리에 '.' 문자열을 다시 넣어준다.

5. 3번의 반복이 정상적으로 끝난 경우, 스도쿠 문자열의 배열이 정상적이지 않은 경우이므로 false를 반환한다.

6. 2번의 반복이 정상적으로 끝난 경우, 스도쿠 문자열의 모든 문자열의 배열이 정상적으로 완료가 되었으므로, true를 반환한다.

7. 각 반환의 결과가 최초 호출의 경우 해당 불리언 값을 주어진 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SudokuSolver.java){:target="_blank"}에서 확인 가능합니다.