---
title: "Leetcode Java Search a 2D Matrix II"
excerpt: "Leetcode Search a 2D Matrix II Java 풀이"
last_modified_at: 2021-11-16T23:00:00
header:
  image: /assets/images/leetcode/search-a-2d-matrix-ii.png
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
[Link](https://leetcode.com/problems/search-a-2d-matrix-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean searchMatrix(int[][] matrix, int target) {
    int row = matrix.length - 1;
    int col = 0;
    while (row >= 0 && col <= matrix[0].length - 1) {
      if (target == matrix[row][col]) {
        return true;
      } else if (target < matrix[row][col]) {
        row--;
      } else if (target > matrix[row][col]) {
        col++;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/588106201/){:target="_blank"}

# 설명
1. 주어진 2차원 배열인 matrix에 target의 값이 존재하는지를 검증하는 문제이다.
- left-right 순으로 배열 내 값들이 오름차순 정렬되어 있다.
- top-bottom 순으로 배열 내 값들이 오름차순 정렬되어 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- 행의 위치를 저장할 row에 마지막 행의 위치인 $matrix.length - 1$를 넣어준다.
- 열의 위치를 저장할 col에 처음 열의 위치인 0을 넣어준다.

3. row가 첫 행인 0보다 크거나 같고, col이 마지막 열인 $matrix[0].length - 1$보다 작거나 같을 때 까지 반복하여 검증을 수행한다.
- target의 값과 matrix[row][col]의 값이 동일한 경우 matrix에 target의 값이 존재하므로, true를 주어진 문제의 결과를 반환한다.
- target의 값이 matrix[row][col]의 값보다 작은 경우, row를 감소시켜 그 위의 행에서 반복을 통해 검증을 계속 수행한다.
  - top-bottom 순으로 배열 내 값들이 오름차순 정렬되어 있으므로, target의 값이 작으면 행을 위로 이동하여 값의 비교를 수행한다.
- target의 값이 matrix[row][col]의 값보다 큰 경우, col을 증가시켜 옆의 행들의 값을 이용하여 검증을 계속 수행한다.
  - left-right 순으로 배열 내 값들이 오름차순 정렬되어 있으므로, target의 값이 크면 열을 우측으로 이동하여 값의 비교를 수행한다.

4. 반복이 완료되면 해당 배열 내 target의 값이 존재하지 않는다는 의미이므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SearchA2DMatrixII.java){:target="_blank"}에서 확인 가능합니다.