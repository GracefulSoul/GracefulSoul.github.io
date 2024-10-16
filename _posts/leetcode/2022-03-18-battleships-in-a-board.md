---
title: "Leetcode Java Battleships in a Board"
excerpt: "Leetcode Battleships in a Board Java 풀이"
last_modified_at: 2022-03-18T12:00:00
header:
  image: /assets/images/leetcode/battleships-in-a-board.png
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
[Link](https://leetcode.com/problems/battleships-in-a-board/){:target="_blank"}

# 코드
```java
class Solution {

  public int countBattleships(char[][] board) {
    int row = board.length;
    int col = board[0].length;
    int count = 0;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (board[i][j] == '.' || (i > 0 && board[i - 1][j] == 'X') || (j > 0 && board[i][j - 1] == 'X')) {
          continue;
        }
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/662239142/){:target="_blank"}

# 설명
1. 주어진 2차원 배열인 board는 해양 위의 전함의 위치를 'X'로 표시되어 있어, 해당 전함의 수를 계산하는 문제이다.
- 단, 전함은 $1 \times k$ 혹은 $k \times 1$ 크기로 존재하며 인접한 전함은 없다고 가정한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row는 board 행의 수를 저장하기 위한 변수로, board의 길이로 초기화한다.
- col은 board 열의 수를 저장하기 위한 변수로, board[0]의 길이로 초기화한다.
- count는 전함의 수를 저장하기 위한 변수로, 0으로 초기화한다.

3. board 배열을 첫 셀에서 마지막 셀까지 반복하여 아래를 수행한다.
- 아래의 경우 개수 산정에 의미가 없으므로 무시하고 계속 수행한다.
  - board[i][j]가 '.'이면 비어있으므로 개수 산정에서 제외한다.
  - i가 0보다 큰 상황에서 좌측 셀의 값이 'X'인 경우 $k \times 1$ 크기의 전함이므로 개수 산정에서 제외한다.
  - j가 0보다 큰 상황에서 아래 셀의 값이 'x'인 경우 $1 \times k$ 크기의 전함이므로 개수 산정에서 제외한다.
- 위의 경우를 제외하면 전함이 새로 발견되었으므로 count를 증가시킨다.

4. 반복이 완료되면 전함의 개수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BattleshipsInABoard.java){:target="_blank"}에서 확인 가능합니다.