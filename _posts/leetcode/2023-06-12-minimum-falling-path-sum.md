---
title: "Leetcode Java Minimum Falling Path Sum"
excerpt: "Leetcode Minimum Falling Path Sum Java"
last_modified_at: 2023-06-12T21:50:00
header:
  image: /assets/images/leetcode/minimum-falling-path-sum.png
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
[Link](https://leetcode.com/problems/minimum-falling-path-sum){:target="_blank"}

# 코드
```java
class Solution {

  public int minFallingPathSum(int[][] matrix) {
    return this.dfs(matrix, matrix.length - 2);
  }

  private int dfs(int[][] matrix, int index) {
    int length = matrix.length;
    if (index < 0) {
      int result = matrix[0][0];
      for (int i = 1; i < length; i++) {
        result = Math.min(result, matrix[0][i]);
      }
      return result;
    } else {
      for (int i = 0; i < length; i++) {
        int min = matrix[index + 1][i];
        if (i > 0) {
          min = Math.min(min, matrix[index + 1][i - 1]);
        }
        if (i < length - 1) {
          min = Math.min(min, matrix[index + 1][i + 1]);
        }
        matrix[index][i] += min;
      }
      return this.dfs(matrix, index - 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-falling-path-sum/submissions/969588545/){:target="_blank"}

# 설명
1. matrix의 맨 위 행의 임의 열에서 시작하여 대각선 아래를 포함한 아래 방향으로 이동할 때, 숫자들의 합이 최소가 되는 값을 구하는 문제이다.

2. 3번에서 정의한 dfs(int[][] matrix, int index) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 값을 탐색할 dfs(int[][] matrix, int index) 메서드를 정의한다.
- length는 matrix의 길이를 저장할 변수이다.
- index가 음수인 경우, 탐색이 완료되었으므로 matrix의 첫 행의 값들 중 가장 작은 값을 반환한다.
- index가 양수이면 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
  - min에 matrix[$index + 1$][i]의 값을 넣어준다.
  - i가 0보다 큰 경우, min에 min과 대각선 좌측 아래 값인 matrix[$index + 1$][$i - 1$]의 값 중 작은 값을 넣어준다.
  - i가 $length - 1$보다 작은 경우, min에 min과 대각선 우측 아래 값인 matrix[$index + 1$][$i + 1$]의 값 중 작은 값을 넣어준다.
  - matrix[index][i]의 위치에 아래로 이동할 때 최소 값인 min을 더해준다.
- 반복이 완료되면 index위치에 $index - 1$을 넣어 재귀 호출한 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumFallingPathSum.java){:target="_blank"}에서 확인 가능합니다.