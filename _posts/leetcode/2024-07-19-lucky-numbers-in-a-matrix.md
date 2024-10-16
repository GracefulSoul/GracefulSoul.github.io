---
title: "Leetcode Java Lucky Numbers in a Matrix"
excerpt: "Leetcode Lucky Numbers in a Matrix Java"
last_modified_at: 2024-07-19T18:40:00
header:
  image: /assets/images/leetcode/lucky-numbers-in-a-matrix.png
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
[Link](https://leetcode.com/problems/lucky-numbers-in-a-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> luckyNumbers(int[][] matrix) {
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < matrix.length; i++) {
      int index = this.getIndexOfMinValue(matrix[i]);
      int value = matrix[i][index];
      if (this.checkMaxValue(matrix, index, value)) {
        result.add(value);
      }
    }
    return result;
  }

  private int getIndexOfMinValue(int[] row) {
    int index = 0;
    for (int i = 1, min = row[index]; i < row.length; i++) {
      if (row[i] < min) {
        min = row[i];
        index = i;
      }
    }
    return index;
  }

  private boolean checkMaxValue(int[][] matrix, int i, int value) {
    for (int[] row : matrix) {
      if (row[i] > value) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/lucky-numbers-in-a-matrix/submissions/1326095011/){:target="_blank"}

# 설명
1. 각자 다른 값을 가진 $m \times n$ 크기의 2차원 배열이 주어지면 행의 최솟값이면서 열의 최댓값인 값을 모두 찾는 문제이다.

2. result는 결과를 저장할 변수로, ArrayList로 초기화한다.

3. 0부터 matrix의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- index에 matrix[i]의 값 중 최솟값의 위치를 넣어준다.
- value에 matrix[i][index]의 값을 넣어준다.
- value가 matrix의 index번째 열의 최댓값이면 조건을 만족하므로, result에 value를 넣어준다.

4. 반복이 완료되면 조건을 만족하는 값들을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LuckyNumbersInAMatrix.java){:target="_blank"}에서 확인 가능합니다.