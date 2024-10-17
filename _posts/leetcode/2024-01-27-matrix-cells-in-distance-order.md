---
title: "Leetcode Java Matrix Cells in Distance Order"
excerpt: "Leetcode Easy - 'Matrix Cells in Distance Order' 문제 Java 풀이"
last_modified_at: 2024-01-27T19:30:00
header:
  image: /assets/images/leetcode/matrix-cells-in-distance-order.png
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
[Link](https://leetcode.com/problems/matrix-cells-in-distance-order){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] allCellsDistOrder(int rows, int cols, int rCenter, int cCenter) {
    int[][] result = new int[rows * cols][];
    result[0] = new int[] { rCenter, cCenter };
    int index = 1;
    int max = Math.max(rCenter, rows - rCenter - 1) + Math.max(cCenter, cols - cCenter - 1);
    for (int i = 1; i <= max; i++) {
      int row = rCenter - i;
      int col = cCenter;
      for (int j = i; j > 0; j--) {
        if (row >= 0 && col >= 0) {
          result[index++] = new int[] { row, col };
        }
        row++;
        col--;
      }
      for (int j = i; j > 0; j--) {
        if (row < rows && col >= 0) {
          result[index++] = new int[] { row, col };
        }
        row++;
        col++;
      }
      for (int j = i; j > 0; j--) {
        if (row < rows && col < cols) {
          result[index++] = new int[] { row, col };
        }
        row--;
        col++;
      }
      for (int j = i; j > 0; j--) {
        if (row >= 0 && col < cols) {
          result[index++] = new int[] { row, col };
        }
        row--;
        col--;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/matrix-cells-in-distance-order/submissions/1158150449/){:target="_blank"}

# 설명
1. $rows \times cols$ 크기의 2차원 배열 내 [rCenter, cCenter] 위치에서 가장 가까운 거리부터 먼 거리까지 순서대로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 가까운 거리 순서대로 저장할 배열로, 가능한 셀의 갯수인 $rows \times cols$ 크기의 2차원 정수 배열로 초기화하고 첫 값을 시작 위치인 [rCenter, cCenter]를 넣어준다.
- index는 result에 저장할 위치 값을 저장할 변수로, 첫 값이 포함되었으므로 1로 초기화한다.
- max는 현재 위치인 [rCenter, cCenter]에서 모서리까지 가장 먼 거리를 저장할 변수로, rCenter와 $rows - rCenter - 1$인 행의 최대 이동거리 중 큰 값과 cCenter와 $cols - cCenter - 1$ 중 큰 값을 더해서 넣어준다.

3. 1부터 max 이하까지 i를 증가시키며 아래를 반복한다.
- row에 $rCenter - i$를, col에 cCenter를 넣어준다.
- 위-좌측의 대각선 방향으로 탐색하기 위해서 i부터 0 초과까지 j를 감소시키며 아래를 수행한다.
  - [row, col] 위치가 배열 내에 존재하는 0 이상인 경우, result[index]에 [row, col] 위치를 넣고 index를 증가시킨다.
  - 위치 이동을 위해서 row를 증가시키고, col을 감소시킨다.
- 좌측-아래의 대각선 방향으로 탐색하기 위해서 i부터 0 초과까지 j를 감소시키며 아래를 수행한다.
  - [row, col] 위치가 배열 내에 존재하는 row가 rows 미만이면서 col이 0 이상인 경우, result[index]에 [row, col] 위치를 넣고 index를 증가시킨다.
  - 위치 이동을 위해서 row와 col을 증가시킨다.
- 아래-우측의 대각선 방향으로 탐색하기 위해서 i부터 0 초과까지 j를 감소시키며 아래를 수행한다.
  - [row, col] 위치가 배열 내에 존재하는 row가 rows 미만이면서 col이 colse 미만인 경우, result[index]에 [row, col] 위치를 넣고 index를 증가시킨다.
  - 위치 이동을 위해서 row를 감소시키고, col을 증가시킨다.
- 우측-위의 대각선 방향으로 탐색하기 위해서 i부터 0 초과까지 j를 감소시키며 아래를 수행한다.
  - [row, col] 위치가 배열 내에 존재하는 row가 0 이상이면서 col이 colse 미만인 경우, result[index]에 [row, col] 위치를 넣고 index를 증가시킨다.
  - 위치 이동을 위해서 row와 col을 감소시킨다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MatrixCellsInDistanceOrder.java){:target="_blank"}에서 확인 가능합니다.