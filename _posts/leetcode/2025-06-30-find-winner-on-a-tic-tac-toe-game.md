---
title: "Leetcode Java Find Winner on a Tic Tac Toe Game"
excerpt: "Leetcode - 'Find Winner on a Tic Tac Toe Game' 문제 Java 풀이"
last_modified_at: 2025-06-30T21:55:00
header:
  image: /assets/images/leetcode/find-winner-on-a-tic-tac-toe-game.png
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
[Link](https://leetcode.com/problems/find-winner-on-a-tic-tac-toe-game/){:target="_blank"}

# 코드
```java
class Solution {

  public String tictactoe(int[][] moves) {
    int length = 3;
    int[] rows = new int[length];
    int[] cols = new int[length];
    int diagonal1 = 0;
    int diagonal2 = 0;
    int player = 1;
    for (int[] move : moves) {
      rows[move[0]] += player;
      cols[move[1]] += player;
      diagonal1 = move[0] == move[1] ? diagonal1 + player : diagonal1;
      diagonal2 = move[0] + move[1] == length - 1 ? diagonal2 + player : diagonal2;
      if (Math.abs(rows[move[0]]) == length
          || Math.abs(cols[move[1]]) == length
          || Math.abs(diagonal1) == length
          || Math.abs(diagonal2) == length) {
        return player == 1 ? "A" : "B";
      }
      player *= -1;
    }
    return moves.length < 9 ? "Pending" : "Draw";
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-winner-on-a-tic-tac-toe-game/submissions/1681368781/){:target="_blank"}

# 설명
1. A와 B가 $3 \times 3$ 크기의 바둑판에서 가로, 세로, 대각선이 한 줄을 완성하는 게임을 할 때, 누가 이겼는지 플레이어를 반환하는 문제이다.
- A 먼저 시작하고, B는 그 다음으로 순서를 번걸아가면서 둔다.
- 마지막까지 수행한 결과, 이긴 사람이 없는 경우 "Draw"를 반환한다.
- 아직 마지막까지 수행하지 않은 경우, "Pending"을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 바둑판 길이인 3을 저장한 변수이다.
- rows와 cols는 행과 열의 값을 저장하기 위한 변수로, 각각 length 크기의 정수 배열로 초기화한다.
- diagonal1, diagonal2는 왼쪽 아래에서 오른쪽 위로, 왼쪽 위에서 오른쪽 아래로 연결된 대각선 내 돌의 갯수를 저장하기 위한 변수로, 둘 다 0으로 초기화한다.
- player는 각 플레이어를 구분하기 위한 값으로, A를 뜻하는 1로 초기화한다.

3. moves의 처음 값부터 각 값을 move에 순차적으로 넣어 아래를 수행한다.
- rows 내 move[0]인 x축, move[1]인 y축에 각각 플레이어의 값인 player를 더해준다.
- diagonal1에 move[0]과 move[1]이 동일한 왼쪽 아래에서 오른쪽 위로 향하는 대각선의 위치 값이면 $diagonal1 + player$인 player의 돌이 계속 이어지는지를, 아니면 diagonal1 값 그대로 유지한다.
- diagonal2에 $move[0] + move[1]$의 값이 $length - 1$과 동일한 왼쪽 위에서 오른쪽 아래로 향하는 대각선의 위치 값이면 $diagonal2 + player$를, 아니면 diagonal2 값 그대로 유지한다.
- 아래의 각 값이 length와 동일한 하나라도 선이 완성된 경우 player가 1이면 "A"를, -1인 그 외의 경우 "B"를 주어진 문제의 결과로 반환한다.
  - rows[move[0]]의 절댓값인 move[0] 행이 player 돌로 채워진 경우.
  - cols[move[1]]의 절댓값인 move[1] 열이 player 돌로 채워진 경우.
  - diagonal1의 절댓값인 왼쪽 아래에서 오른쪽 위로 향하는 대각선이 player 돌로 채워진 경우.
  - diagonal2의 절댓값인 왼쪽 위에서 오른쪽 아래로 향하는 대각선이 player 돌로 채워진 경우.
- 수행을 완료하고 player에 -1을 곱하여 플레이어를 전환한다.

4. 반복이 완료되면 moves의 길이가 9 미만인 진행 중이면 "Pending"을, 9인 수행이 완료되었으면 "Draw"를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindWinnerOnATicTacToeGame.java){:target="_blank"}에서 확인 가능합니다.