---
title: "Leetcode Java Number of Submatrices That Sum to Target"
excerpt: "Leetcode Hard - 'Number of Submatrices That Sum to Target' 문제 Java 풀이"
last_modified_at: 2024-01-28T10:20:00
header:
  image: /assets/images/leetcode/number-of-submatrices-that-sum-to-target.png
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
[Link](https://leetcode.com/problems/number-of-submatrices-that-sum-to-target){:target="_blank"}

# 코드
```java
class Solution {

  public int numSubmatrixSumTarget(int[][] matrix, int target) {
    int row = matrix.length;
    int col = matrix[0].length;
    int result = 0;
    for (int i = 0; i < row; i++) {
      int[] dp = new int[col];
      for (int j = i; j < row; j++) {
        for (int k = 0; k < col; k++) {
          dp[k] += matrix[j][k];
        }
        for (int l = 0; l < col; l++) {
          int sum = 0;
          for (int m = l; m < col; m++) {
            sum += dp[m];
            if (sum == target) {
              result++;
            }
          }
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-submatrices-that-sum-to-target/submissions/1158705432/){:target="_blank"}

# 설명
1. matrix 내 부분 배열 내 값들의 합이 target이 되는 부분 배열의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 행과 열의 갯수를 저장할 변수이다.
- result는 부분 배열의 갯수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 row 미만까지 i를 증가시키며 아래를 수행한다.
- dp는 합계 계산을 돕기 위한 배열로, col 크기의 정수로 초기화한다.
- i부터 row 미만까지 j를 증가시키며 아래를 수행한다.
  - 0부터 col 미만까지 k를 증가시키며, dp[k]의 값에 matrix[j][k]의 값을 누계한다.
  - 0부터 col 미만까지 l을 증가시키며, sum을 초기화 한 후 l부터 col 미만까지 m을 증가시키며 sum에 dp[m]의 값을 더해서 sum과 target이 동일한 경우 조건을 충족하므로 result를 증가시켜준다.

4. 반복이 완료되면 조건을 만족하는 부분 배열의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfSubmatricesThatSumToTarget.java){:target="_blank"}에서 확인 가능합니다.