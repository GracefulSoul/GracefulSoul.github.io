---
title: "Leetcode Java Surface Area of 3D Shapes"
excerpt: "Leetcode Surface Area of 3D Shapes Java"
last_modified_at: 2023-04-03T20:20:00
header:
  image: /assets/images/leetcode/surface-area-of-3d-shapes.png
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
[Link](https://leetcode.com/problems/surface-area-of-3d-shapes){:target="_blank"}

# 코드
```java
class Solution {

  public int surfaceArea(int[][] grid) {
    int result = 0;
    int length = grid.length;
    for (int i = 0; i < length; i++) {
      for (int j = 0; j < length; j++) {
        if (grid[i][j] > 0) {
          result += (grid[i][j] * 4) + 2;
        }
        if (i > 0) {
          result -= Math.min(grid[i][j], grid[i - 1][j]) * 2;
        }
        if (j > 0) {
          result -= Math.min(grid[i][j], grid[i][j - 1]) * 2;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/surface-area-of-3d-shapes/submissions/927158316/){:target="_blank"}

# 설명
1. 정육면체의 큐브의 갯수가 담긴 $n \times n$ 크기인 grid를 3차원으로 구성할 때 면적을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 면적을 계산할 변수로, 0으로 초기화한다.
- length는 grid의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키고, 다시 0부터 length 미만까지 j를 증가시키며 아래를 수행한다.
- grid[i][j]의 값이 존재하면 result에 grid[i][j]를 4로 곱한 전후좌우의 네 변의 값에 위와 아래인 2를 더해서 넣어준다.
- i가 0보다 큰 경우, result에 grid[i][j]와 grid[$i - 1$][j] 중 작은 겹친 면적에 2를 곱해서 빼준다.
- j도 0보다 큰 경우, result에 grid[i][j]와 grid[i][$j - 1$] 중 작은 겹친 면적에 2를 곱해서 빼준다.

4. 반복이 완료되면 면적이 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SurfaceAreaOf3DShapes.java){:target="_blank"}에서 확인 가능합니다.