---
title: "Leetcode Java Longest Increasing Path in a Matrix"
excerpt: "Leetcode Longest Increasing Path in a Matrix Java 풀이"
last_modified_at: 2022-01-05T18:00:00
header:
  image: /assets/images/leetcode/longest-increasing-path-in-a-matrix.png
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
[Link](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestIncreasingPath(int[][] matrix) {
    int row = matrix.length;
    int col = matrix[0].length;
    int[][] memory = new int[row][col];
    int result = 0;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        result = Math.max(result, this.recursive(matrix, memory, i, j, row, col));
      }
    }
    return result;
  }

  private int recursive(int[][] matrix, int[][] memory, int i, int j, int row, int col) {
    if (memory[i][j] > 0) {
      return memory[i][j];
    }
    int num = matrix[i][j];
    int result = 0;
    if (i > 0 && matrix[i - 1][j] > num) {
      result = Math.max(result, this.recursive(matrix, memory, i - 1, j, row, col));
    }
    if (i + 1 < row && matrix[i + 1][j] > num) {
      result = Math.max(result, this.recursive(matrix, memory, i + 1, j, row, col));
    }
    if (j > 0 && matrix[i][j - 1] > num) {
      result = Math.max(result, this.recursive(matrix, memory, i, j - 1, row, col));
    }
    if (j + 1 < col && matrix[i][j + 1] > num) {
      result = Math.max(result, this.recursive(matrix, memory, i, j + 1, row, col));
    }
    memory[i][j] = ++result;
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/613487541/){:target="_blank"}

# 설명
1. 주어진 정수 배열인 matrix를 이용하여 해당 위치의 값보다 이동한 위치의 값이 큰 값으로 이동하는 경우, 가능한 최대 이동 거리를 반환하는 문제이다.
- 각 셀에서 상, 하, 좌, 우 네 방향으로만 움직일 수 있다.
- 대각선으로 이동하거나 배열 밖으로 움직일 수 없다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row은 matrix의 행의 개수를 저장하기 위한 변수로, matirx.length를 넣어준다.
- col은 matrix의 열의 개수를 저장하기 위한 변수로, matrix[0].length를 넣어준다.
- memory는 matrix를 이용하여 이동하는 경우, 최대 이동 거리를 기억하기 위한 임시 배열이다.
- result는 matrix를 순회하여 최대 이동 거리를 저장하기 위한 변수이다.

3. matrix를 순회하여 result에 최대 이동 거리를 저장한다.
- result에 result와 4번에서 정의한 recursive(matrix, memory, i, j, row, col) 메서드의 수행 결과 중 큰 값을 넣어준다.

4. [DFS(Depth-first search)](https://en.wikipedia.org/wiki/Depth-first_search){:target="_blank"} 알고리즘을 이용하여 최대 이동거리를 구할 recursive(int[][] matrix, int[][] memory, int i, int j, int row, int col) 메서드를 정의한다.
- memory[i][j]의 값이 0보다 큰 경우 이미 최대 이동 거리를 계산한 위치이므로, 해당 값을 반환한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - num은 matrix[i][j]의 값 저장할 변수이다.
  - result는 최대 이동 거리를 계산하기 위한 변수로, 0으로 초기화한다.
- i가 0보다 크고 matrix[$i - 1$][j]의 값이 num보다 큰 경우, result에 result와 좌측의 위치인 $i - 1$로 재귀 호출한 결과 중 큰 값을 넣어준다.
- $i + 1$이 row보다 작고 matrix[$i + 1][j]의 값이 num보다 큰 경우, result에 result와 우측의 위치인 $i + 1$로 재귀 호출한 결과 중 큰 값을 넣어준다.
- j가 0보다 크고 matrix[i][$j - 1$] 값이 num보다 큰 경우, result에 result와 아래의 위치인 $j - 1$로 재귀 호출한 결과 중 큰 값을 넣어준다.
- $j + 1$이 col보다 작고 matrix[i][j + 1]의 값이 num보다 큰 경우, result에 result와 위의 위치인 $j + 1$로 재귀 호출한 결과 중 큰 값을 넣어준다.
- result를 증가시키고 memory[i][j]의 위치에 값을 넣고, 반환시킨다.

5. 반복이 완료되어 matrix를 이용하여 값이 증가하며 이동하는 최대 이동 거리가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestIncreasingPathInAMatrix.java){:target="_blank"}에서 확인 가능합니다.