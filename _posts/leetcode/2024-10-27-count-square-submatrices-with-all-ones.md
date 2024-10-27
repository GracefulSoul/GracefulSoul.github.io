---
title: "Leetcode Java Count Square Submatrices with All Ones"
excerpt: "Leetcode - 'Count Square Submatrices with All Ones' 문제 Java 풀이"
last_modified_at: 2024-10-27T10:00:00
header:
  image: /assets/images/leetcode/count-square-submatrices-with-all-ones.png
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
[Link](https://leetcode.com/problems/count-square-submatrices-with-all-ones/){:target="_blank"}

# 코드
```java
class Solution {

  public int countSquares(int[][] matrix) {
    int result = 0;
    int row = matrix.length;
    int col = matrix[0].length;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (matrix[i][j] > 0 && i > 0 && j > 0) {
          matrix[i][j] = Math.min(matrix[i - 1][j - 1], Math.min(matrix[i - 1][j], matrix[i][j - 1])) + 1;
        }
        result += matrix[i][j];
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-square-submatrices-with-all-ones/submissions/1434725813/){:target="_blank"}

# 설명
1. matrix에 1로 이루어진 정사각형의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 갯수를 계산하기 위한 변수로, 0으로 초기화한다.
- row와 col은 matrix는 행과 열을 저장한 변수이다.

3. i는 0부터 row 미만까지 j는 0부터 col 미만까지 i와 j를 증가시키면서 아래를 반복한다.
- matirx[i][j]의 위치에 아래 중 가장 작은 값에 1을 더한 값을 넣어준다.
  - matrix[$i - 1$][$j - 1$]
  - matrix[$i - 1$][j]
  - matrix[i][$j - 1$]
- result에 matirx[i][j]의 값을 더해준다.

4. 반복이 완료되면 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountSquareSubmatricesWithAllOnes.java){:target="_blank"}에서 확인 가능합니다.