---
title: "Leetcode Java Maximal Square"
excerpt: "Leetcode Maximal Square Java 풀이"
last_modified_at: 2021-10-27T12:00:00
header:
  image: /assets/images/leetcode/maximal-square.png
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
[Link](https://leetcode.com/problems/maximal-square/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximalSquare(char[][] matrix) {
    int max = 0;
    int row = matrix.length;
    int col = matrix[0].length;
    int[][] dp = new int[row + 1][col + 1];
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (matrix[i][j] == '1') {
          dp[i + 1][j + 1] = Math.min(dp[i][j], Math.min(dp[i][j + 1], dp[i + 1][j])) + 1;
          max = Math.max(max, dp[i + 1][j + 1]);
        }
      }
    }
    return max * max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/577742027/){:target="_blank"}

# 설명
1. 주어진 2차원 배열 matrix를 이용하여 정사각형 모양인 1로 구성된 부분 배열의 최대 크기를 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 1로 이루어진 부분 배열의 최대 길이를 저장하기 위한 변수로, 0으로 초기화한다.
- row는 matrix 행의 개수를 저장한다.
- col는 matrix 열의 개수를 저장한다.
- dp는 1로 이루어진 부분 배열의 최대 크기를 구하기 위한 DP로, 크기를 matrix보다 하나 큰 [$row + 1$][$col + 1$]로 초기화한다.

3. matrix를 순회하여 dp를 이용하여 max의 값을 넣어준다.
- matrix[i][j]의 값이 '1'인 경우 아래를 수행한다.
  - dp[$i + 1$][$j + 1$]에 dp[i][j], dp[i][$j + 1$], dp[$i + 1$][j] 값 중 가장 작은 값을 찾아 해당 부분 배열이 동일한 값인지를 검증하고 1을 더한 값을 넣어준다.
  - max에 max와 dp[$i + 1$][$j + 1$] 값 중 큰 값을 넣어 정사각형 모양인 1로 구성된 부분 배열 한 변의 길이를 넣어준다.

4. 반복이 완료되면 정사각형 모양인 1로 구성된 부분 배열 한 변의 길이를 저장한 max를 이용하여 $max \times max$를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximalSquare.java){:target="_blank"}에서 확인 가능합니다.