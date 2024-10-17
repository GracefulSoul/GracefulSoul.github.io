---
title: "Leetcode Java Island Perimeter"
excerpt: "Leetcode - 'Island Perimeter' 문제 Java 풀이"
last_modified_at: 2022-04-22T12:00:00
header:
  image: /assets/images/leetcode/island-perimeter.png
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
[Link](https://leetcode.com/problems/island-perimeter/){:target="_blank"}

# 코드
```java
class Solution {

  public int islandPerimeter(int[][] grid) {
    int border = 0;
    for (int i = 0; i < grid.length; i++) {
      for (int j = 0; j < grid[0].length; j++) {
        if (grid[i][j] == 1) {
          border += 4;
          if (i > 0 && grid[i - 1][j] == 1) {
            border -= 2;
          }
          if (j > 0 && grid[i][j - 1] == 1) {
            border -= 2;
          }
        }
      }
    }
    return border;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/685110245/){:target="_blank"}

# 설명
1. 섬의 지도 역할을 하는 grid의 섬 둘레를 구하는 문제이다.
- 육지는 $grid[i][j] = 1$, 해상은 $grid[i][j] = 0$으로 표현한다.

2. 섬의 둘레를 계산할 border를 0으로 정의한다.

3. 0부터 grid의 행 개수 전까지 i를 증가시키며, 0부터 grid의 열 개수 전까지 j를 증가시키며 아래를 반복한다.
- grid[i][j]의 값이 육지인 1인 경우 아래를 수행한다.
  - 해당 위치가 육지이므로, 둘레를 4 증가시킨다.
  - i가 0 초과이며 해당 위치의 좌측 칸인 grid[$i - 1$][j]의 값이 1이면 두 육지가 연결되는 지점을 두 육지에서 제거해야 하므로, border를 2 감소시킨다. (예를 들어, 육지 한 칸의 둘레는 4이고, 육지 두 칸의 둘레는 6이다.)
  - j가 0 초과이며 해당 위치의 위 칸인 grid[i][$j - 1$]의 값이 1이면 위와 동일한 이유로, border를 2 감소시킨다.

4. 반복이 완료되면 계산된 섬의 둘레를 저장한 border를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IslandPerimeter.java){:target="_blank"}에서 확인 가능합니다.