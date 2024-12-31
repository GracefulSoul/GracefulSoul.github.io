---
title: "Leetcode Java Queens That Can Attack the King"
excerpt: "Leetcode - 'Queens That Can Attack the King' 문제 Java 풀이"
last_modified_at: 2024-12-31T10:40:00
header:
  image: /assets/images/leetcode/queens-that-can-attack-the-king.png
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
[Link](https://leetcode.com/problems/queens-that-can-attack-the-king/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[][] DIRECTIONS = {
    { -1, -1 },
    { 0, -1 },
    { 1, -1 },
    { 1, 0 },
    { 1, 1 },
    { 0, 1 },
    { -1, 1 },
    { -1, 0 }
  };

  public List<List<Integer>> queensAttacktheKing(int[][] queens, int[] king) {
    boolean[][] visited = new boolean[8][8];
    for (int[] queen : queens) {
      visited[queen[0]][queen[1]] = true;
    }
    List<List<Integer>> result = new ArrayList<>();
    for (int[] direction : DIRECTIONS) {
      for (int x = king[0] + direction[0], y = king[1] + direction[1];
          0 <= x && x < 8 && 0 <= y && y < 8; x += direction[0], y += direction[1]) {
        if (visited[x][y]) {
          result.add(Arrays.asList(x, y));
          break;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/queens-that-can-attack-the-king/submissions/1492929507/){:target="_blank"}

# 설명
1. $8 \times 8$ 크기의 체스판에서 queens 위치의 여왕들과 king 위치의 왕이 존재할 때, 왕을 직접 공격할 수 있는 여왕의 좌표를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- DIRECTIONS은 여왕이 움직일 수 있는 8방면 좌표를 저장한 전역 변수로, 현재 위치에서 각 방면으로 이동하기 위한 x와 y축 이동 값을 저장한다.
- visited는 여왕과 만날 수 있는 위치를 저장할 변수로, $8 \times 8$ 크기의 정수 배열로 초기화하여 queens의 각 위치에 true를 넣어 표시해준다.
- result는 만날 수 있는 여왕 위치를 저장할 변수로, ArrayList로 초기화한다.

3. DIRECTIONS의 각 값을 direction에 순차적으로 넣어 아래를 수행한다.
- x는 $king[0] + direction[0]$, y는 $king[1] + direction[1]$로 초기화하여 체스 판 위에서 움직일 수 있을 때 까지 x에 direction[0]을, y에 direction[1]을 더하면서 아래를 반복한다.
  - visited[x][y]의 값이 true인 여왕과 만나는 경우, result에 해당 위치를 넣고 다음 위치의 여왕들은 해당 위치의 여왕에 막혀 공격이 불가능하므로 현재 반복을 중지한다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/QueensThatCanAttackTheKing.java){:target="_blank"}에서 확인 가능합니다.