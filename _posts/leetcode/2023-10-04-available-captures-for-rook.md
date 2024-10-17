---
title: "Leetcode Java Available Captures for Rook"
excerpt: "Leetcode Easy - 'Available Captures for Rook' 문제 Java 풀이"
last_modified_at: 2023-10-04T19:10:00
header:
  image: /assets/images/leetcode/available-captures-for-rook.png
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
[Link](https://leetcode.com/problems/available-captures-for-rook){:target="_blank"}

# 코드
```java
class Solution {

  private int[][] directions = new int[][] {
    { 0, 1 },
    { 1, 0 },
    { 0, -1 },
    { -1, 0 }
  };

  public int numRookCaptures(char[][] board) {
    for (int i = 0; i < 8; i++) {
      for (int j = 0; j < 8; j++) {
        if (board[i][j] == 'R') {
          return this.numRookCaptures(board, i, j, directions[0])
             + this.numRookCaptures(board, i, j, directions[1])
             + this.numRookCaptures(board, i, j, directions[2])
             + this.numRookCaptures(board, i, j, directions[3]);
        }
      }
    }
    return 0;
  }

  private int numRookCaptures(char[][] board, int x, int y, int[] direction) {
    while (x >= 0 && x < 8 && y >= 0 && y < 8 && board[x][y] != 'B') {
      if (board[x][y] == 'p') {
        return 1;
      } else {
        x += direction[0];
        y += direction[1];
      }
    }
    return 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/available-captures-for-rook/submissions/1066689028/){:target="_blank"}

# 설명
1. $8 \times 8$ 크기의 체스판에서 아래의 체스말들로 흰 룩이 잡을 수 있는 검정색 폰의 갯수를 구하는 문제이다.
- 체스판의 각 공간의 값은 아래와 같다.
  - 'R'은 흰색 룩을 의미한다.
  - 'B'는 흰색 비숍을 의미한다.
  - 'p'는 검정색 폰을 의미한다.
  - '.'은 빈 공간을 의미한다.
- 룩은 네 방향(북, 동, 남, 서) 중 하나의 방향으로 원하는 횟수만큼 이동이 가능하며, 아래의 경우 멈춘다.
  - 체스판의 끝인 경우.
  - 검정색 폰을 잡은 경우.
  - 흰색 비숍이 앞에 있는 경우.

2. 전역 변수인 directions는 룩의 이동 방향을 저장할 변수로, 북동남서 순으로 [x, y] 좌표를 넣어 초기화한다.

3. 0부터 8미만까지 i를, 0부터 8미만까지 y를 증가시키며 아래를 반복한다.
- board[i][j]가 'R'인 흰색 룩인 경우, 4번에서 정의한 numRookCaptures(char[][] board, int x, int y, int[] direction) 메서드를 수행한 결과를 directions의 순서대로 수행한 결과의 합을 주어진 문제의 결과로 반환한다.

4. 주어진 좌표인 [x, y]에서 이동 방향인 direction을 이동하며 잡을 수 있는 검정색 폰을 탐색하기 위한 numRookCaptures(char[][] board, int x, int y, int[] direction) 메서드를 정의한다.
- x와 y가 0 ~ 7 범위 내까지 board[x][y]가 'B'인 흰색 비숍이 아닌 경우일 때까지 아래를 반복한다.
  - board[x][y]가 'p'인 검정색 폰인 경우, 잡은 횟수인 1을 반환한다.
  - 위의 경우가 아니라면 direction 방향으로 x와 y를 더한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AvailableCapturesForRook.java){:target="_blank"}에서 확인 가능합니다.