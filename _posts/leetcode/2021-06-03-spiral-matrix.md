---
title: "Leetcode Java Spiral Matrix"
excerpt: "Leetcode Spiral Matrix Java 풀이"
last_modified_at: 2021-06-03T19:40:00
header:
  image: /assets/images/leetcode/spiral-matrix.png
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
[Link](https://leetcode.com/problems/spiral-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSubArray(int[] nums) {
    List<Integer> result = new ArrayList<>();
    int rowSize = matrix.length;
    int colSize = matrix[0].length;
    int row = 0;
    int col = 0;
    int rowMax = rowSize - 1;
    int colMax = colSize - 1;
    while (result.size() < rowSize * colSize) {
      for (int idx = col; idx <= colMax && result.size() < rowSize * colSize; idx++) {
        result.add(matrix[row][idx]);
      }
      for (int idx = row + 1; idx <= rowMax - 1 && result.size() < rowSize * colSize; idx++) {
        result.add(matrix[idx][colMax]);
      }
      for (int idx = colMax; idx >= col && result.size() < rowSize * colSize; idx--) {
        result.add(matrix[rowMax][idx]);
      }
      for (int idx = rowMax - 1; idx >= row + 1 && result.size() < rowSize * colSize; idx--) {
        result.add(matrix[idx][col]);
      }
      row++;
      col++;
      rowMax--;
      colMax--;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/502357804/){:target="_blank"}

# 설명
1. 주어진 배열 matrix를 외각부터 중심까지 순차적으로 숫자를 이어주는 문제이다.

2. 아래의 기본 변수들을 정의한다.
- 변수 rowSize는 주어진 배열 matrix의 가로 길이이다.
- 변수 colSize는 주어진 배열 matrix의 세로 길이이다.
- 변수 row는 주어진 배열 matrix의 가로 시작 인덱스이다.
- 변수 col은 주어진 배열 matrix의 세로 시작 인덱스이다.
- 변수 rowMax는 주어진 배열 matrix의 가로 마지막 인덱스이다.
- 변수 colMax는 주어진 배열 matrix의 세로 마지막 인덱스이다.

3. 순차적으로 숫자를 이어 넣은 result의 크기가 배열의 크기가 될 때 까지 반복하여 결과를 만들어준다.
- col과 row 단위의 각 배열의 가장 바깥 값들을 한 줄씩 차례대로 넣는다.
  - 우측 -> 아래 -> 좌측 -> 위 순으로 값들을 result에 넣는다.
  - 한 바퀴를 돌고 나서, 한 칸씩 내부로 이동하기 위해 변수 row와 col은 증가시키고, rowMax와 colMax는 감소시킨다.
- 가장 바깥 값들을 넣으면 다시 반복하여 다음 바깥 값들을 한 줄씩 차례대로 넣는다.

4. 반복이 종료되면 주어진 배열 matrix를 외각부터 중심까지 순차적으로 숫자를 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SpiralMatrix.java){:target="_blank"}에서 확인 가능합니다.