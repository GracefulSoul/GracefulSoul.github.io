---
title: "Leetcode Java Diagonal Traverse"
excerpt: "Leetcode Diagonal Traverse Java"
last_modified_at: 2022-05-19T19:00:00
header:
  image: /assets/images/leetcode/diagonal-traverse.png
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
[Link](https://leetcode.com/problems/diagonal-traverse/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findDiagonalOrder(int[][] mat) {
    int row = 0;
    int col = 0;
    int rowLength = mat.length;
    int colLength = mat[0].length;
    int[] result = new int[rowLength * colLength];
    for (int idx = 0; idx < result.length; idx++) {
      result[idx] = mat[row][col];
      if ((row + col) % 2 == 0) {
        if (col == colLength - 1) {
          row++;
        } else if (row == 0) {
          col++;
        } else {
          row--;
          col++;
        }
      } else {
        if (row == rowLength - 1) {
          col++;
        } else if (col == 0) {
          row++;
        } else {
          row++;
          col--;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/702683026/){:target="_blank"}

# 설명
1. mat의 모든 값들을 아래의 규칙을 만족하는 하나의 배열로 반환하는 문제이다.
- 첫 값의 위치부터 우측 위로 시작하여 다음 값이 없을 경우, 우측 혹은 아래 칸으로 이동해서 좌측 아래로 숫자들을 차례대로 나열한다.
- 좌측 아래로 이동하다가 다음 값이 없을 경우, 아래 혹은 우측 칸으로 이동해서 우측 위로 숫자들을 나열한다.
- 위의 두 규칙을 반복하여 모든 값을 하나의 배열에 넣어준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 mat의 행과 열을 탐색할 위지 변수로, 모두 0으로 초기화한다.
- rowLength와 colLength는 mat의 행과 열의 길이를 저장할 변수로, 각 길이로 초기화한다.
- result는 모든 값을 순차적으로 이어줄 배열로, rowLength와 colLength를 곱한 값의 크기로 초기화한다.
- 0부터 result의 길이 미만까지 idx를 증가시키며 아래를 수행한다.
  - result의 idx번째 위치에 mat[row][col] 값을 넣어준다.
  - row와 col을 더한 값이 짝수인 경우, col이 마지막 열이면 row를 증가시키고 row가 첫 행이면 col을 증가시키고 그 외의 경우 row를 감소시키고 col을 증가시켜 우측 위 방향으로 위치를 이동시킨다.
  - row와 col을 더한 값이 홀수인 경우, row가 마지막 행이면 col을 증가시키고 col이 첫 열이면 row를 증가시키고 그 외의 경우 row를 증가시키고 col을 감소시켜 좌측 아래 방향으로 위치를 이동시킨다.

3. 반복이 완료되면 위의 규칙대로 대각선으로 이동하여 값을 이어준 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DiagonalTraverse.java){:target="_blank"}에서 확인 가능합니다.