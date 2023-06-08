---
title: "Leetcode Java Count Negative Numbers in a Sorted Matrix"
excerpt: "Leetcode Count Negative Numbers in a Sorted Matrix Java"
last_modified_at: 2023-06-08T19:50:00
header:
  image: /assets/images/leetcode/count-negative-numbers-in-a-sorted-matrix.png
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
[Link](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix){:target="_blank"}

# 코드
```java
class Solution {

  public int countNegatives(int[][] grid) {
    int result = 0;
    int row = grid.length;
    int col = grid[0].length;
    for (int i = 0, right = col - 1; i < row; i++) {
      int left = 0;
      while (left <= right) {
        int mid = left + ((right - left) / 2);
        if (grid[i][mid] < 0) {
          right = mid - 1;
        } else {
          left = mid + 1;
        }
      }
      result += col - left;
      right = left - 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/submissions/966557036/){:target="_blank"}

# 설명
1. 행과 열 별로 감소하는 추세인 $m \times n$ 크기의 grid 내 음수인 값의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 grid 내 음수인 값의 갯수를 저장할 변수로, 0으로 초기화한다.
- row와 col은 행과 열의 길이를 저장한 변수이다.

3. 0부터 row 미만까지 i를 증가하며, right에 $col - 1$을 넣고 아래를 반복한다.
- left를 0으로 초기화 하고 left가 right 미만일 때 까지 아래를 반복한다.
  - mid에 $left + \frac{right - left}{2}$인 중앙값을 넣어준다.
  - grid[i][mid]의 값이 음수인 경우, right에 $mid - 1$을 넣어 범위를 좁혀준다.
  - grid[i][mid]의 값이 양수인 경우, left에 $mid + 1$을 넣어 범위를 좁혀준다.
- 반복이 종료되면 result에 $col - left$인 음수의 갯수를 넣어준다.
- 아래로 내려갈수록 값은 감소하므로, right에 $left - 1$을 넣어 다음 탐색 범위를 좁혀준다.

4. 모든 반복이 완료되면 grid 내 음수의 갯수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountNegativeNumbersInASortedMatrix.java){:target="_blank"}에서 확인 가능합니다.