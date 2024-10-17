---
title: "Leetcode Java Range Sum Query 2D - Immutable"
excerpt: "Leetcode - 'Range Sum Query 2D - Immutable' 문제 Java 풀이"
last_modified_at: 2021-12-17T18:00:00
header:
  image: /assets/images/leetcode/range-sum-query-2d-immutable.png
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
[Link](https://leetcode.com/problems/range-sum-query-2d-immutable/){:target="_blank"}

# 코드
```java
class NumMatrix {

  private int[][] matrix;

  public NumMatrix(int[][] matrix) {
    this.matrix = matrix;
    int rowLength = matrix.length;
    int colLength = matrix[0].length;
    for (int i = 0; i < rowLength; i++) {
      int sum = matrix[i][0];
      for (int j = 1; j < colLength; j++) {
        sum += matrix[i][j];
        matrix[i][j] = sum;
      }
    }
    for (int j = 0; j < colLength; j++) {
      int sum = matrix[0][j];
      for (int i = 1; i < rowLength; i++) {
        sum += matrix[i][j];
        matrix[i][j] = sum;
      }
    }
  }

  public int sumRegion(int row1, int col1, int row2, int col2) {
    int sum = matrix[row2][col2];
    if (row1 > 0) {
      sum -= matrix[row1 - 1][col2];
    }
    if (col1 > 0) {
      sum -= matrix[row2][col1 - 1];
    }
    if (row1 > 0 && col1 > 0) {
      sum += matrix[row1 - 1][col1 - 1];
    }
    return sum;
  }

}

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix obj = new NumMatrix(matrix);
 * int param_1 = obj.sumRegion(row1,col1,row2,col2);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/603086157/){:target="_blank"}

# 설명
1. 2차원 배열을 주입하여 부분 배열 값의 합을 구하는 NumArray 클래스를 완성하는 문제이다.
- 생성자인 NumArray(int[][] matrix)는 NumsArray 클래스를 초기화하여 nums의 값들을 주입한다.
- 메서드인 sumRegion(int row1, int col1, int row2, int col2)은 생성자로 주입된 배열에서 row1 ~ row2, col1 ~ col2의 부분 배열에 속하는 값들의 합을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- matrix는 생성자로 부여된 배열의 값을 넣을 변수이다.

3. 생성자인 NumArray(int[][] matrix)를 완성한다.
- 주어진 matrix를 전역 변수인 matrix에 넣어준다.
- rowLength와 colLength에 matirx의 행과 열의 길이를 넣어준다.
- matrix를 반복하여 첫 행의 값들을 기준으로 아래 행으로 내려가면서 누계하고 해당 값을 위치에 넣어준다.
- matrix를 반복하여 첫 열의 값들을 기준으로 우측 열로 이동하면서 누계하고 해당 값을 위치에 넣어준다.

4. 메서드인 sumRegion(int row1, int col1, int row2, int col2)을 완성한다.
- sum에 matrix[row2][col2] 값을 넣어준다.
- row1이 0보다 큰 경우, sum에서 matrix[$row1 - 1$][col2] 값을 빼준다.
- col1이 0보다 큰 경우, sum에서 matrix[row2][$col1 - 1$] 값을 빼준다.
- row1과 col1 둘 다 0보다 큰 경우, sum에서 matrix[$row1 - 1$][$col1 - 1$] 값을 빼준다.
- 위의 경우의 수를 제거한 부분 배열의 합인 sum을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RangeSumQuery2DImmutable.java){:target="_blank"}에서 확인 가능합니다.