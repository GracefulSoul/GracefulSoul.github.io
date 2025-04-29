---
title: "Leetcode Java N-Queens II"
excerpt: "Leetcode - 'N-Queens II' 문제 Java 풀이"
last_modified_at: 2025-04-29T19:40:00
header:
  image: /assets/images/leetcode/n-queens-ii.png
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
[Link](https://leetcode.com/problems/n-queens-ii/){:target="_blank"}

# 코드
```java
class Solution {

  private int count;

  public int totalNQueens(int n) {
    this.count = 0;
    int diagonalLength = 2 * n;
    this.backtracking(n, 0, new boolean[n], new boolean[diagonalLength], new boolean[diagonalLength]);
    return this.count;
  }

  private void backtracking(int n, int i, boolean[] values, boolean[] diagonal1, boolean[] diagonal2) {
    if (i == n) {
      this.count++;
    } else {
      for (int j = 0; j < n; j++) {
        int index1 = j - i + n;
        int index2 = j + i;
        if (!values[j] && !diagonal1[index1] && !diagonal2[index2]) {
          values[j] = diagonal1[index1] = diagonal2[index2] = true;
          this.backtracking(n, i + 1, values, diagonal1, diagonal2);
          values[j] = diagonal1[index1] = diagonal2[index2] = false;
        }
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/n-queens-ii/submissions/1621007254/){:target="_blank"}

# 설명
1. 이전 문제 [N-Queens](../n-queens){:target="_blank"}와 유사한 문제로, n개의 퀸이 $n \times n$ 크기의 2차원 배열 위에 서로 공격할 수 없는 위치에 존재할 수 있는 경우의 수를 구하는 문제이다.

2. 전역 변수인 count는 경우의 수를 계산하기 위한 변수로 0으로 초기화 후, 대각선으로 진행하기 위한 최대 길이인 diagonalLength를 $2 \times n$으로 초기화한다.

3. 백트래킹 방식으로 경우의 수를 계산할 backtracking(int n, int i, boolean[] values, boolean[] diagonal1, boolean[] diagonal2) 메서드를 정의한다.
- i가 n인 마지막 행의 경우, count를 증가시킨다.
- i가 n이 아닌 경우, 0부터 n 미만까지 j를 증가시키며 아래를 반복한다.
  - 각 대각선의 이동 위치인 index1에 $j - i + n$을, index2에 $j + i$를 넣어준다.
  - values[j], diagonal1[index1], diagonal2[index2]의 값이 모두 false인 방문하지 않은 위치의 경우, 해당 값에 true를 넣어 방문한 이력을 넣고 $i + 1$을 넣어 재귀 호출을 수행한 후 다시 앞의 위치에 true를 넣어 복구해준다.

4. 반복이 완료되면 경우의 수가 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NQueensII.java){:target="_blank"}에서 확인 가능합니다.