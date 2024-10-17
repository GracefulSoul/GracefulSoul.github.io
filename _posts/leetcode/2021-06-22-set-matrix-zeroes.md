---
title: "Leetcode Java Set Matrix Zeroes"
excerpt: "Leetcode - 'Set Matrix Zeroes' 문제 Java 풀이"
last_modified_at: 2021-06-22T17:00:00
header:
  image: /assets/images/leetcode/set-matrix-zeroes.png
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
[Link](https://leetcode.com/problems/set-matrix-zeroes/){:target="_blank"}

# 코드
```java
class Solution {

  public void setZeroes(int[][] matrix) {
    this.setZeroesDownTop(matrix, this.setZeroesTopDown(matrix));
  }

  private boolean setZeroesTopDown(int[][] matrix) {
    boolean isFirstColumnZero = false;
    for (int i = 0; i < matrix.length; i++) {
      if (matrix[i][0] == 0) {
        isFirstColumnZero = true;
      }
      for (int j = 1; j < matrix[0].length; j++) {
        if (matrix[i][j] == 0) {
          matrix[i][0] = matrix[0][j] = 0;
        }
      }
    }
    return isFirstColumnZero;
  }

  private void setZeroesDownTop(int[][] matrix, boolean isFirstColumnZero) {
    for (int i = matrix.length - 1; i >= 0; i--) {
      for (int j = matrix[0].length - 1; j >= 1; j--) {
        if (matrix[i][0] == 0 || matrix[0][j] == 0) {
          matrix[i][j] = 0;
        }
      }
      if (isFirstColumnZero) {
        matrix[i][0] = 0;
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/511399634/){:target="_blank"}

# 설명
1. 주어진 배열 matrix 내부에 0이 존재하는 열과 행의 모든 값에 0을 채우는 문제이다.
- 단, matrix를 내부에서 변경해야하므로 [In-Place 알고리즘](https://en.wikipedia.org/wiki/In-place_algorithm){:target="_blank"}을 이용하여 변경해야 한다.

2. 주어진 배열 matrix 내부에 0이 존재하는지 반복문을 통해 위에서 아래로 이동하며 확인한다.
- 첫 열이 0인 경우, isFirstColumnZero를 true로 바꾸어준다.
- 두 번째 열부터는 matrix[i][j]의 값이 0인 경우, matrix[i][0]와 matrix[0][j]를 0으로 넣어주어 해당 열과 행을 0으로 바꿀 준비를 한다.
- 반복이 종료되면 isFirstColumnZero를 다음 함수로 전달한다.

3. 주어진 배열 matrix를 반복하여 내부에 0이 존재하는 행과 열에 0을 채워주어 주어진 문제의 풀이를 완료한다.
- matrix[i][0] 혹은 matrix[0][j]가 0인 경우, 2번에서 0을 넣는 행과 열에 포함된 위치이므로 matrix[i][j]에 0을 넣어준다.
- 만일 isFirstcolumnZero가 true인 경우, 첫 열이 모두 0이 된다는 의미이므로 matrix[i][0]에 0을 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EditDistance.java){:target="_blank"}에서 확인 가능합니다.