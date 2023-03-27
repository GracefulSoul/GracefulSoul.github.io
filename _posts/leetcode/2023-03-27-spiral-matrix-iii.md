---
title: "Leetcode Java Spiral Matrix III"
excerpt: "Leetcode Spiral Matrix III Java"
last_modified_at: 2023-03-27T19:10:00
header:
  image: /assets/images/leetcode/spiral-matrix-iii.png
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
[Link](https://leetcode.com/problems/spiral-matrix-iii){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
    int[][] result = new int[rows * cols][2];
    int row = 0;
    int col = 1;
    int n = 0;
    for (int j = 0; j < rows * cols; n++) {
      for (int i = 0; i < (n / 2) + 1; i++) {
        if (0 <= rStart && rStart < rows && 0 <= cStart && cStart < cols) {
          result[j++] = new int[] { rStart, cStart };
        }
        rStart += row;
        cStart += col;
      }
      int temp = row;
      row = col;
      col = -temp;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/spiral-matrix-iii/submissions/922926207/){:target="_blank"}

# 설명
1. $rows \times cols$ 크기의 2차원 배열의 [rStart, cStart]에서 시작하여 오른쪽 -> 아래쪽 -> 왼쪽 -> 위쪽으로 시계 방향의 나선형으로 이동하는 위치를 반환하는 문제이다.
- 배열 밖으로 벗어나는 경우, 나선형으로 이동하여 배열 안으로 들어오는 위치로 이어진다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 넣을 배열로, $rows \times cols$ 크기의 2차원 정수 배열로 초기화한다.
- row와 col은 방향을 결정할 변수로, 오른쪽으로 이동하므로 0과 1로 초기화한다.
- n은 같은 방향으로 이동 횟수를 계산 할 변수로, 0으로 초기화한다.

3. j가 0부터 $rows \times cols$ 미만까지 n을 증가시키며 아래를 반복한다.
- 0부터 $\frac{n}{2} + 1$까지 i를 증가시키며 아래를 반복한다.
  - [rStart, cStart]가 배열 내 위치인 경우, result의 j번쨰 위치에 [rStart, cStart]를 넣어주고 j를 증가시킨다.
  - rStart에 row를, cStart의 col을 더해 다음 위치로 이동한다.
- 나선 방향으로 변환하기 위하여 row에 col을, col을 -row 값으로 바꾸어준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SpiralMatrixIII.java){:target="_blank"}에서 확인 가능합니다.