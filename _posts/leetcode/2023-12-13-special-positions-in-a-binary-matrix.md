---
title: "Leetcode Java Special Positions in a Binary Matrix"
excerpt: "Leetcode MaxiSpecial Positions in a Binary Matrix Java"
last_modified_at: 2023-12-13T22:50:00
header:
  image: /assets/images/leetcode/special-positions-in-a-binary-matrix.png
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
[Link](https://leetcode.com/problems/special-positions-in-a-binary-matrix){:target="_blank"}

# 코드
```java
class Solution {

  public int numSpecial(int[][] mat) {
    int row = mat.length;
    int col = mat[0].length;
    int[] rowSum = new int[row];
    int[] colSum = new int[col];
    int result = 0;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (mat[i][j] == 1) {
          rowSum[i]++;
          colSum[j]++;
        }
      }
    }
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (mat[i][j] == 1 && rowSum[i] == 1 && colSum[j] == 1) {
          result++;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/special-positions-in-a-binary-matrix/submissions/1118861470/){:target="_blank"}

# 설명
1. mat 배열 내 상하좌우의 모든 값의 합이 1인 셀의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 mat의 행과 열의 수를 저장한 변수이다.
- rowSum과 colSum은 행과 열 별 합을 구하기 위한 변수로, row와 col 크기의 정수 배열로 초기화한다.
- result는 셀의 갯수를 저장할 변수로, 0으로 초기화한다.

3. mat의 모든 값을 반복하여 rowSum에는 행의 위치 별 합을, colSum에는 열의 위치 별 합을 넣어준다.

4. mat[i][j], rowSum, colSum 모두 1인 조건을 만족하는 셀들을 모두 result에 더한 후 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SpecialPositionsInABinaryMatrix.java){:target="_blank"}에서 확인 가능합니다.