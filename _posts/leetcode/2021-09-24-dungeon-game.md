---
title: "Leetcode Java Dungeon Game"
excerpt: "Leetcode - 'Dungeon Game' 문제 Java 풀이"
last_modified_at: 2021-09-24T12:00:00
header:
  image: /assets/images/leetcode/dungeon-game.png
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
[Link](https://leetcode.com/problems/dungeon-game/){:target="_blank"}

# 코드
```java
class Solution {

  public int calculateMinimumHP(int[][] dungeon) {
    int row = dungeon.length;
    int col = dungeon[0].length;
    int[][] health = new int[row][col];
    for (int i = row - 1; i >= 0; i--) {
      for (int j = col - 1; j >= 0; j--) {
        if (i == row - 1 && j == col - 1) {
          health[i][j] = Math.max(1, 1 - dungeon[i][j]);
        } else if (i == row - 1) {
          health[i][j] = Math.max(health[i][j + 1] - dungeon[i][j], 1);
        } else if (j == col - 1) {
          health[i][j] = Math.max(health[i + 1][j] - dungeon[i][j], 1);
        } else {
          health[i][j] = Math.min(Math.max(health[i + 1][j] - dungeon[i][j], 1), Math.max(health[i][j + 1] - dungeon[i][j], 1));
        }
      }
    }
    return health[0][0];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/559997771/){:target="_blank"}

# 설명
1. 주어진 2차원 배열인 dungeon을 이용하여 dungeon[0][0]에서 dungeon[$dungeon.length - 1$][$dungeon[0].length - 1$]에 도달하기까지 숫자들의 합이 양의 정수가 되는 최소한의 health를 찾는 문제이다.
- 단, 이동은 오른쪽과 아래로만 가능하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row는 주어진 2차원 배열 dungeon 행의 개수를 저장한 변수이다.
- col은 주어진 2차원 배열 dungeon 열의 개수를 저장한 변수이다.
- health는 주어진 2차원 배열 dungeon을 탐색할 때 필요한 health를 산정하기 위해 사용될 2차원 배열로, dungeon과 동일한 크기로 선언한다.

3. dungeon[$row - 1$][$col - 1$]부터 시작해서 역순으로 탐색에 필요한 최소한의 health를 구한다.
- 시작 위치인 dungeon[$row - 1$][$col - 1$]인 경우, 1과 $1 - dungeon[i][j]$ 중 큰 값을 넣어준다.
- i가 마지막 행인 $row - 1$인 경우, 우측 값에서 현재 값을 뺀 값과 1 중 큰 값을 넣어준다.
- j가 마지막 열인 $col - 1$인 경우, 아래 값에서 현재 값을 뺀 값과 1 중 큰 값을 넣어준다.
- 그 외의 경우, 우측 값에서 현재 값을 뺀 값과 1중 큰 값과 아래 값에서 현재 값을 뺀 값과 1 중 큰 값 중 작은 값을 넣어준다.

4. 반복이 완료되면 health[0][0]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DungeonGame.java){:target="_blank"}에서 확인 가능합니다.