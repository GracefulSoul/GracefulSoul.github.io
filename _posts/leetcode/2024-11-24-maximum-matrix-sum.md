---
title: "Leetcode Java Maximum Matrix Sum"
excerpt: "Leetcode - 'Maximum Matrix Sum' 문제 Java 풀이"
last_modified_at: 2024-11-24T10:20:00
header:
  image: /assets/images/leetcode/maximum-matrix-sum.png
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
[Link](https://leetcode.com/problems/maximum-matrix-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public long maxMatrixSum(int[][] matrix) {
    int row = matrix.length;
    int col = matrix[0].length;
    long result = 0;
    long negative = 0;
    long min = Long.MAX_VALUE;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (matrix[i][j] < 0) {
          negative++;
        }
        int absolute = Math.abs(matrix[i][j]);
        result += absolute;
        min = Math.min(min, absolute);
      }
    }
    if (negative % 2 == 0) {
      return result;
    } else {
      return result - (2 * min);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-matrix-sum/submissions/1461212166/){:target="_blank"}

# 설명
1. 정사각형 모양의 matrix에 아래의 연산을 이용하여 계산한 합계가 최대인 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 행과 열의 길이를 저장한 변수이다.
- result는 합계를 저장할 변수로, 0으로 초기화한다.
- negative는 음수의 갯수를 계산할 변수로, 0으로 초기화한다.
- min은 최솟값을 저장할 변수로, Long의 가장 큰 값으로 초기화한다.

3. 0부터 row 미만까지 i를 증가시키고, 0부터 col 미만까지 j를 증가시키며 아래를 반복한다.
- matrix[i][j]의 값이 음수라면 nagative 값을 증가시킨다.
- absolute는 matrix의 절댓값을 넣어준다.
- result에 absolute를 더해준 후 min에 min과 absolute 중 작은 값을 넣어준다.

4. negative가 짝수인지 여부에 따라 아래 결과를 반환한다.
- 짝수인 음수가 모두 양수로 전환되는 경우, result를 주어진 문제의 결과로 반환한다.
- 홀수인 한 값이 음수로 존재하는 경우, result에 가장 작은 값이 저장된 min을 2로 곱한 값을 빼준 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumMatrixSum.java){:target="_blank"}에서 확인 가능합니다.