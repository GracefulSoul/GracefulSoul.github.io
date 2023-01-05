---
title: "Leetcode Java Valid Tic-Tac-Toe State"
excerpt: "Leetcode Valid Tic-Tac-Toe State Java"
last_modified_at: 2023-01-05T20:45:00
header:
  image: /assets/images/leetcode/valid-tic-tac-toe-state.png
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
[Link](https://leetcode.com/problems/valid-tic-tac-toe-state){:target="_blank"}

# 코드
```java
class Solution {

  public boolean validTicTacToe(String[] board) {
    int diff = 0;
    for (int i = 0; i < 3; i++) {
      for (int j = 0; j < 3; j++) {
        if (board[i].charAt(j) == 'X') {
          diff++;
        }
        if (board[i].charAt(j) == 'O') {
          diff--;
        }
      }
    }
    return !((diff != 0 && diff != 1) || (this.isWin(board, 'X') && diff == 0) || (this.isWin(board, 'O') && diff == 1));
  }

  private boolean isWin(String[] board, char c) {
    return (board[0].charAt(0) == c && board[0].charAt(1) == c && board[0].charAt(2) == c)
        || (board[1].charAt(0) == c && board[1].charAt(1) == c && board[1].charAt(2) == c)
        || (board[2].charAt(0) == c && board[2].charAt(1) == c && board[2].charAt(2) == c)
        || (board[0].charAt(0) == c && board[1].charAt(0) == c && board[2].charAt(0) == c)
        || (board[0].charAt(1) == c && board[1].charAt(1) == c && board[2].charAt(1) == c)
        || (board[0].charAt(2) == c && board[1].charAt(2) == c && board[2].charAt(2) == c)
        || (board[0].charAt(0) == c && board[1].charAt(1) == c && board[2].charAt(2) == c)
        || (board[0].charAt(2) == c && board[1].charAt(1) == c && board[2].charAt(0) == c);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/valid-tic-tac-toe-state/submissions/871904979/){:target="_blank"}

# 설명
1. 'O', 'X', '' 문자로 이루어진 $3 \times 3$ 크기의 Tic-Tac-Toe 보드를 이용하여 아래의 규칙을 이용한 게임이 유효하게 종료될 수 있는지를 검증하는 문제이다.
- '' 문자는 빈 공간을 의미하며, 첫 번째 플레이어는 'X' 문자로 두 번째 플레이어는 'O' 문자로 시작한다.
- 'X'와 'O' 문자는 빈 공간인 ''에 들어갈 수 있으며, 채워진 값은 바뀌지 않는다.
- 행, 열, 대각선에 'X' 혹은 'O' 문자가 동일하게 들어간 경우, 게임은 종료된다.
- 모든 빈 값에 값이 채워지면 게임은 종료되며, 더 이상 값을 변경할 수 없다.

2. diff는 'X'와 'O'의 갯수의 차이를 저장할 변수로, 0으로 초기화하고 board의 모든 값을 이용하여 'X'는 값을 더하고 'O'는 값을 빼준다.

3. 아래의 경우에 하나라도 해당하는 경우 규칙을 만족하지 않으므로 false를, 모두 만족하지 않으면 true를 주어진 문제의 결과로 반환한다.
- 'X'와 'O'의 갯수가 동일하지 않으며 'X'가 하나 더 많지 않은 경우.
  - 플레이어가 정상적으로 번갈아 두는 경우, 'X'가 하나 더 많거나 'X'와 'O'는 동일한 갯수가 된다.
- 4번의 isWin(String[] board, char c) 메서드를 board와 'X'로 수행한 결과가 true면서, 'X'와 'O'의 갯수가 동일한 경우.
  - 첫 번째 플레이어가 이기게 되면, 자신의 차례를 통해 'X'를 하나 추가한 상태이므로 'X'가 하나 더 많아야한다.
- 4번의 isWin(String[] board, char c) 메서드를 board와 'O'로 수행한 결과가 true면서, 'O'의 갯수가 하나 더 많은 경우.
  - 두 번째 플레이어가 이기게 되면, 자신의 차례를 통해 'O'를 하나 추가한 상태이므로 'O'와 'X'의 갯수가 동일해야한다.

4. board에서 c 문자를 둔 플레이어가 이기는 경우를 검증하기 위한 isWin(String[] board, char c) 메서드를 정의한다.
- c 문자열이 가로/세로/대각선 모든 경우의 수 중 하나라도 만족하면 true를, 아니면 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidTicTacToeState.java){:target="_blank"}에서 확인 가능합니다.