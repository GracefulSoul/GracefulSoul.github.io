---
title: "Leetcode Java Toeplitz Matrix"
excerpt: "Leetcode Toeplitz Matrix Java"
last_modified_at: 2022-12-16T13:00:00
header:
  image: /assets/images/leetcode/toeplitz-matrix.png
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
[Link](https://leetcode.com/problems/toeplitz-matrix){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isToeplitzMatrix(int[][] matrix) {
    for (int i = 0; i < matrix.length - 1; i++) {
      for (int j = 0; j < matrix[i].length - 1; j++) {
        if (matrix[i][j] != matrix[i + 1][j + 1]) {
          return false;
        }
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/toeplitz-matrix/submissions/860485188/){:target="_blank"}

# 설명
1. $m \times n$ 크기의 matrix가 [Toeplitz matrix](https://en.wikipedia.org/wiki/Toeplitz_matrix){:target="_blank"}인지 검증하는 문제이다.

2. Toeplitz matrix는 좌측 아래로 이어지는 대각선 상 존재하는 모든 값이 동일한 숫자로 존재해야 하므로, 모든 값을 반복하여 좌측 하단의 값이 동일하지 않으면 false를 주어진 문제의 결과로 반환한다.

3. 검증이 완료되면 Toeplitz matrix이므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ToeplitzMatrix.java){:target="_blank"}에서 확인 가능합니다.