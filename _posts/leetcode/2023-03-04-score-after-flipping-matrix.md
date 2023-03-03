---
title: "Leetcode Java Score After Flipping Matrix"
excerpt: "Leetcode Score After Flipping Matrix Java"
last_modified_at: 2023-03-04T06:50:00
header:
  image: /assets/images/leetcode/score-after-flipping-matrix.png
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
[Link](https://leetcode.com/problems/score-after-flipping-matrix){:target="_blank"}

# 코드
```java
class Solution {

  public int matrixScore(int[][] grid) {
    int row = grid.length;
    int col = grid[0].length;
    int result = (1 << (col - 1)) * row;
    for (int j = 1; j < col; j++) {
      int same = 0;
      for (int i = 0; i < row; i++) {
        if (grid[i][j] == grid[i][0]) {
          same++;
        }
      }
      result += Math.max(same, row - same) * (1 << (col - 1 - j));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/score-after-flipping-matrix/submissions/908592902/){:target="_blank"}

# 설명
1. grid의 값을 이용하여 행과 열의 값을 반전시켜 얻을 수 있는 최대 점수를 구하는 문제이다.
- 각 행의 값은 이진법으로 점수를 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 grid 내 행과 열의 길이를 저장한 변수이다.
- result는 결과를 저장하기 위한 변수로, 행의 마지막 위치 값이 모두 1인 경우 가질 수 있는 값을 넣어준다.

3. 1부터 col 미만까지 j를 증가시키며 아래를 수행한다.
- same은 현재 위치까지 동일한 값의 수를 저장할 변수로, 0으로 초기화한다.
- 0부터 row 미만까지 i를 증가시키며 아래를 수행한다.
  - grid의[i][j]의 값과 grid의[i][0]의 값이 동일하면 same을 증가시켜 동일한 값의 수를 저장한다.
- result에 same 혹은 $row - same$ 중 큰 값인 1로 만들 값의 수와 이진수의 값을 계산하기 위한 $col - 1 - j$의 비트를 좌측으로 한 칸 이동시킨 값의 곱을 더해준다.

4. 반복이 완료되면 계산된 최대 점수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ScoreAfterFlippingMatrix.java){:target="_blank"}에서 확인 가능합니다.