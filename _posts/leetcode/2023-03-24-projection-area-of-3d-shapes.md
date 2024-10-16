---
title: "Leetcode Java Projection Area of 3D Shapes"
excerpt: "Leetcode Projection Area of 3D Shapes Java"
last_modified_at: 2023-03-24T20:30:00
header:
  image: /assets/images/leetcode/projection-area-of-3d-shapes.png
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
[Link](https://leetcode.com/problems/projection-area-of-3d-shapes){:target="_blank"}

# 코드
```java
class Solution {

  public int projectionArea(int[][] grid) {
    int result = 0;
    int length = grid.length;
    for (int i = 0; i < length; i++) {
      int x = 0;
      int y = 0;
      for (int j = 0; j < length; j++) {
        x = Math.max(x, grid[i][j]);
        y = Math.max(y, grid[j][i]);
        if (grid[i][j] > 0) {
          result++;
        }
      }
      result += x + y;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/projection-area-of-3d-shapes/submissions/921266447/){:target="_blank"}

# 설명
1. 크기의 3차원 공간에서 위치 별 $1 \times 1 \times 1$ 큐브를 쌓은 수가 저장된 $n \times n$ 크기의 grid를 이용하여 x, y, z 축 기준으로 볼 때 면적의 합을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 면적의 합을 저장할 변수로, 0으로 초기화한다.
- length는 grid의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
- x와 y는 x축과 y축에서 본 면적을 저장하기 위한 변수로, 모두 0으로 초기화한다.
- 0부터 length 미만까지 j를 증가시키며 아래를 수행한다.
  - x에 해당 값과 grid[i][j]의 값 중 큰 값을 넣어, x축에서 본 i번째 큐브의 최대 면적을 찾는다.
  - y에 해당 값과 grid[j][i]의 값 중 큰 값을 넣어, y축에서 본 j번째 큐브의 최대 면적을 찾는다.
  - grid[i][j]의 값이 0보다 큰 경우, result를 증가시켜 z축에서 본 면적을 증가시킨다.
- 반복이 완료되면 result에 x와 y 값을 더해준다.

4. 모든 반복이 완료되면 면적이 계산된 result를 주어진 문제의 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ProjectionAreaOf3DShapes.java){:target="_blank"}에서 확인 가능합니다.