---
title: "Leetcode Java Flip Columns For Maximum Number of Equal Rows"
excerpt: "Leetcode Medium - 'Flip Columns For Maximum Number of Equal Rows' 문제 Java 풀이"
last_modified_at: 2024-04-03T18:10:00
header:
  image: /assets/images/leetcode/flip-columns-for-maximum-number-of-equal-rows.png
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
[Link](https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxEqualRowsAfterFlips(int[][] matrix) {
    int result = 0;
    int row = matrix.length;
    int col = matrix[0].length;
    int[] temp = new int[col];
    for (int i = 0; i < row; i++) {
      int count = 0;
      for (int j = 0; j < col; j++) {
        temp[j] = 1 - matrix[i][j];
      }
      for (int k = i; k < row; k++) {
        if (Arrays.equals(matrix[k], matrix[i]) || Arrays.equals(matrix[k], temp)) {
          count++;
        }
      }
      result = Math.max(result, count);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows/submissions/1221966298/){:target="_blank"}

# 설명
1. matrix의 임의 열들 내 값들을 0에서 1로 혹은 1에서 0으로 뒤집을 때, 모든 값이 동일한 행의 최대 갯수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 플립 이후에 모든 값이 동일한 행의 최대 갯수를 저장할 변수로, 0으로 초기화한다.
- row와 col은 matrix의 행과 열의 길이를 저장한 변수이다.
- temp는 플립하기 위한 임시 배열로, col 크기의 정수 배열로 초기화한다.

3. 0부터 row 미만까지 i를 증가시키며 아래를 수행한다.
- count는 i번째 수행에 대해서 결과 값을 저장할 변수로, 0으로 초기화한다.
- 0부터 col 미만까지 j를 증가시키며, temp의 각 위치에 값을 뒤집어 넣어준다.
- i부터 row 미만까지 k를 증가시키며, matrix[k]와 matrix[i] 혹은 matrix[k]와 temp가 동일한 값으로 구성된 경우 count를 증가시켜준다.
- result에 result와 count 중 큰 값을 넣어준다.

4. 반복이 완료되면 최대 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlipColumnsForMaximumNumberOfEqualRows.java){:target="_blank"}에서 확인 가능합니다.