---
title: "Leetcode Java Sort Matrix by Diagonals"
excerpt: "Leetcode - 'Sort Matrix by Diagonals' 문제 Java 풀이"
last_modified_at: 2025-08-28T20:30:00
header:
  image: /assets/images/leetcode/sort-matrix-by-diagonals.png
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
[Link](https://leetcode.com/problems/sort-matrix-by-diagonals/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] sortMatrix(int[][] grid) {
    int length = grid.length;
    for (int i = 0; i < length; i++) {
      this.sortDiagonal(grid, i, 0, false);
    }
    for (int j = 1; j < length; j++) {
      this.sortDiagonal(grid, 0, j, true);
    }
    return grid;
  }

  private void sortDiagonal(int[][] grid, int row, int col, boolean isAscending) {
    int length = grid.length - (isAscending ? col : row);
    Integer[] diagonal = new Integer[length];
    for (int i = row, j = col, k = 0; k < length; i++, j++, k++) {
      diagonal[k] = grid[i][j];
    }
    if (isAscending) {
      Arrays.sort(diagonal);
    } else {
      Arrays.sort(diagonal, Collections.reverseOrder());
    }
    for (int num : diagonal) {
      grid[row++][col++] = num;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sort-matrix-by-diagonals/submissions/1751230240/){:target="_blank"}

# 설명
1. grid 내 좌측 상단에서 우측 하단 대각선 방향으로 두 구역을 분리했을 때 각 경우에 따라 대각선 내 값을 정렬하는 문제이다.
- 중앙 대각선 라인을 포함한 좌측 하단 구역은, 좌측 상단에서 우측 하단 대각선 방향으로 값을 내림차순 정렬한다.
- 중앙 대각선 우측 상단 구역은, 좌측 상단에서 우측 하단 대각선 방향으로 값을 오름차순 정렬한다.

2. length는 grid의 길이를 저장한 변수이다.

3. 대각선 라인의 값을 정렬하기 위한 sortDiagonal(int[][] grid, int row, int col, boolean isAscending) 메서드를 정의한다.
- 정렬에 필요한 변수를 정의한다.
  - length는 대각선 숫자 갯수를 저장할 변수로, grid의 길이에 isAscending이면 col을 아니면 row를 빼준다.
  - diagonal은 대각선의 숫자들을 정혈하기 위한 변수로, 값의 정렬을 위해 length 길이의 Integer 배열로 초기화한다.
- i에 row를 j에 col을 넣고 k는 0부터 length까지 i, j, k를 증가시키며, diagonal[k] 위치에 grid[i][j] 값을 넣어준다.
- diagonal을 isAscending 의 값이 true이면 오름차순, 아니면 내림차순 정렬한다.
- diagonal의 각 값을 순차적으로 num에 넣어 grid[row][col] 위치부터 대각선 방향으로 num을 넣어준다.

4. 0부터 length까지 i를 증가시키며 sortDiagonal(int[][] grid, int row, int col, boolean isAscending) 메서드를 row에 i, col에 0, isAscending에 false를 넣어 대각선 좌측 하단 값들을 정렬해준다.

5. 0부터 length까지 j를 증가시키며 sortDiagonal(int[][] grid, int row, int col, boolean isAscending) 메서드를 row에 0, col에 j, isAscending에 true를 넣어 대각선 우측 상단 값들을 정렬해준다.

6. 반복이 완료되어 정렬된 grid를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortMatrixByDiagonals.java){:target="_blank"}에서 확인 가능합니다.