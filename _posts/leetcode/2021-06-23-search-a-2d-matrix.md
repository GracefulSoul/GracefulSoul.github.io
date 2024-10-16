---
title: "Leetcode Java Set Search a 2D Matrix"
excerpt: "Leetcode Set Search a 2D Matrix Java 풀이"
last_modified_at: 2021-06-23T18:30:00
header:
  image: /assets/images/leetcode/search-a-2d-matrix.png
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
[Link](https://leetcode.com/problems/search-a-2d-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean searchMatrix(int[][] matrix, int target) {
    int i = matrix.length - 1;
    int j = 0;
    while (i >= 0 && j < matrix[0].length) {
      if (matrix[i][j] == target) {
        return true;
      } else if (matrix[i][j] > target) {
        i--;
      } else {
        j++;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/512002972/){:target="_blank"}

# 설명
1. 주어진 정렬된 2차원 배열 matrix에 target 정수가 포함되어 있는지 확인하는 문제이다.

2. 주어진 문제를 풀기 위해서 처음부터 끝까지 탐색하기 위한 기본 변수를 선언한다.
- 변수 i는 배열의 마지막 행의 위치인 $matrix.length - 1$로 선언한다.
- 변수 j는 배열의 처음 열의 위치인 0으로 선언한다.

3. 반복문을 통해 배열의 마지막 행부터 처음 행까지 탐색한다.
- matrix[i][j]의 값이 target과 동일하면 true를 주어진 문제의 결과로 반환한다.
- matrix[i][j]의 값이 target보다 크면 i값을 낮추어 위의 행을 탐색한다.
- matrix[i][j]의 값이 target보다 작으면 j값을 크게 하여 다음 열을 탐색한다.

4. 반복문이 종료되면, target과 동일한 값이 없므으로 주어진 문제의 결과로 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SearchA2DMatrix.java){:target="_blank"}에서 확인 가능합니다.