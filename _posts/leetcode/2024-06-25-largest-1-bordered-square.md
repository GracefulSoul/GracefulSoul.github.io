---
title: "Leetcode Java Largest 1-Bordered Square"
excerpt: "Leetcode Largest 1-Bordered Square Java"
last_modified_at: 2024-06-25T21:40:00
header:
  image: /assets/images/leetcode/largest-1-bordered-square.png
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
[Link](https://leetcode.com/problems/largest-1-bordered-square/){:target="_blank"}

# 코드
```java
class Solution {

  public int largest1BorderedSquare(int[][] grid) {
    int result = 0;
    int row = grid.length;
    int col = grid[0].length;
    int[][] rowDp = new int[row + 1][col + 1];
    int[][] colDp = new int[row + 1][col + 1];
    for (int i = 1; i <= row; i++) {
      for (int j = 1; j <= col; j++) {
        if (grid[i - 1][j - 1] == 0) {
          continue;
        }
        rowDp[i][j] = rowDp[i - 1][j] + 1;
        colDp[i][j] = colDp[i][j - 1] + 1;
        for (int k = Math.min(rowDp[i][j], colDp[i][j]); k >= 1; k--) {
          if (rowDp[i][j + 1 - k] >= k && colDp[i + 1 - k][j] >= k) {
            result = Math.max(result, k * k);
            break;
          }
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-1-bordered-square/submissions/1299805720/){:target="_blank"}

# 설명
1. grid에서 하나의 선으로 이루어진 정사각형의 최대 크기를 반환하는 문제이다.
- grid의 1은 선을, 0은 빈 공간을 의미한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 정사각형의 최대 크기를 저장할 변수로, 0으로 초기화한다.
- row와 col은 grid의 가로 세로의 길이를 저장한 변수이다.
- rowDp와 colDp는 행과 열을 지나가며 정사각형의 크기를 계산하기 위한 변수로, 둘 다 $(row + 1) \times (col + 1)$ 크기의 2차원 배열로 초기화한다.

3. 1부터 row 이하까지 i를, 1부터 col 이하까지 j를 증가시키며 아래를 반복한다.
- gird[$i - 1$][$j - 1$]의 값이 0인 빈 칸인 경우, 다음 반복을 수행한다.
- rowDp[i][j]의 위치에 이전 위치 값인 rowDp[$i - 1$][j]의 값에 1을 더해 넣어준다.
- colDp[i][j]의 위치에 이전 위치 값인 colDp[i][$j - 1$]의 값에 1을 더해 넣어준다.
- k는 rowDp[i][j]의 값과 colDp[i][j]의 값 중 작은 정사각형이 가능한 가장 큰 값부터 1 이상일 때 까지 k를 감소시키며 아래를 반복한다.
  - rowDp[i][$j + 1 - k$]의 값과 colDp[$i + 1 - k$][j]의 값이 k 이상인 정사각형이 가능한 최대 크기인 경우, result에 result와 $k \times k$ 중 큰 값을 넣고 반복을 중지한다.

4. 반복이 완료되면 가능한 정사각형의 최대 크기가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Largest1BorderedSquare.java){:target="_blank"}에서 확인 가능합니다.