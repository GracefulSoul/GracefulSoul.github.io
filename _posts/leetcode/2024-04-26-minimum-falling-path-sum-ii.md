---
title: "Leetcode Java Minimum Falling Path Sum II"
excerpt: "Leetcode Minimum Falling Path Sum II Java"
last_modified_at: 2024-04-26T18:40:00
header:
  image: /assets/images/leetcode/minimum-falling-path-sum-ii.png
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
[Link](https://leetcode.com/problems/minimum-falling-path-sum-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int minFallingPathSum(int[][] grid) {
    int length = grid.length;
    for (int i = 1; i < length; i++) {
      int[] min = this.getMinTwoNumbers(grid[i - 1]);
      for (int j = 0; j < length; j++) {
        if (grid[i - 1][j] == min[0]) {
          grid[i][j] += min[1];
        } else {
          grid[i][j] += min[0];
        }
      }
    }
    int result = Integer.MAX_VALUE;
    for (int num : grid[length - 1]) {
      result = Math.min(result, num);
    }
    return result;
  }

  private int[] getMinTwoNumbers(int[] nums) {
    int[] min = new int[] { Integer.MAX_VALUE, Integer.MAX_VALUE };
    for (int num : nums) {
      if (min[0] > num) {
        min[1] = min[0];
        min[0] = num;
      } else if (min[1] > num) {
        min[1] = num;
      }
    }
    return min;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-falling-path-sum-ii/submissions/1242375372/){:target="_blank"}

# 설명
1. 행과 열의 수가 동일한 grid의 첫 행부터 마지막 행까지 동일한 순서의 열로 이동하지 않으면서 값들의 합이 최소 값가 되는 값을 구하는 문제이다.

2. length는 grid 행의 갯수를 저장한 변수이다.

3. 1부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- min에 grid의 $i - 1$ 행 내 가장 작은 두 값을 구해 넣어준다.
- 0부터 length 미만까지 j를 증가시키며 아래를 반복한다.
  - grid[i - 1][j]의 값이 min[0]의 값과 동일한 순서의 열인 경우, grid[i][j]의 값에 min[1]의 값을 더해준다.
  - 위의 경우가 아니라면, grid[i][j]의 값에 최솟값인 min[0]의 값을 더해준다.

4. 3번의 반복이 완료되면, grid의 마지막 행의 값들 중 가장 작은 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumFallingPathSumII.java){:target="_blank"}에서 확인 가능합니다.