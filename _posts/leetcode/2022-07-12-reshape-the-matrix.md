---
title: "Leetcode Java Reshape the Matrix"
excerpt: "Leetcode - 'Reshape the Matrix' 문제 Java 풀이"
last_modified_at: 2022-07-12T20:00:00
header:
  image: /assets/images/leetcode/reshape-the-matrix.png
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
[Link](https://leetcode.com/problems/reshape-the-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] matrixReshape(int[][] mat, int r, int c) {
    int row = mat.length;
    int col = mat[0].length;
    if (r * c != row * col) {
      return mat;
    }
    int[][] result = new int[r][c];
    for (int idx = 0; idx < r * c; idx++) {
      result[idx / c][idx % c] = mat[idx / col][idx % col];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/745091607/){:target="_blank"}

# 설명
1. MATLAB에서 제공하는 reshape 함수를 구현하는 문제이다.
- reshape 함수는 주어진 2차원 배열을 해당 순서 그대로 $r \tiems c$ 배열로 전환하고, 불가능하면 원래 배열을 그대로 반환하는 함수이다.

2. row에 mat 행의 수를, col에 mat 열의 수를 저장한다.

3. $r \times c$의 값이 $row \times col$와 동일하지 않으면 변환이 불가능하므로, mat를 주어진 문제의 결과로 반환한다.

4. 3번의 경우가 아니라면 $r times c$ 크기의 배열로 변환이 가능하므로, result를 해당 배열 크기로 초기화한다.

5. 0 부터 $r \times c$ 미만까지 idx를 증가시키며 아래를 반복하여 mat의 값들을 순차적으로 result에 넣어준다.
- $\frac{idx}{c}$의 값과 나머지를 이용하여 result[값][나머지]의 위치에, $\frac{idx}{col}$의 값과 나머지를 이용하여 mat[값][나머지]의 값을 넣어준다.

6. 5번을 통해 만들어진 result 배열을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReshapeTheMatrix.java){:target="_blank"}에서 확인 가능합니다.