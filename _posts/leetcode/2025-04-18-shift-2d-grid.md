---
title: "Leetcode Java Shift 2D Grid"
excerpt: "Leetcode - 'Shift 2D Grid' 문제 Java 풀이"
last_modified_at: 2025-04-18T19:10:00
header:
  image: /assets/images/leetcode/shift-2d-grid.png
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
[Link](https://leetcode.com/problems/shift-2d-grid/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> shiftGrid(int[][] grid, int k) {
    int rows = grid.length;
    int cols = grid[0].length;
    int[][] arr = new int[rows][cols];
    for (int i = 0; i < rows; i++) {
      for (int j = 0; j < cols; j++) {
        arr[(i + ((j + k) / cols)) % rows][(j + k) % cols] = grid[i][j];
      }
    }
    List<List<Integer>> result = new ArrayList<>();
    for (int[] row : arr) {
      List<Integer> list = new ArrayList<>();
      for (int col : row) {
        list.add(col);
      }
      result.add(list);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shift-2d-grid/submissions/1610357310/){:target="_blank"}

# 설명
1. 2차원 정수 배열 grid를 이용하여 k번 아래의 규칙대로 수행한 결과를 반환하는 문제이다.
- grid[i][j] 값을 grid[i][$j + 1$] 위치로 이동한다.
- grid[i][$n - 1$]인 오른쪽 마지막 위치의 값은 grid[$i + 1$][0] 위치로 이동한다.
- grid[$m - 1$][$n - 1$] 마지막 모서리 값은 처음 위치인 grid[0][0] 위치로 이동한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- rows와 cols는 grid의 행과 열의 갯수를 저장한 변수이다.
- arr은 조건에 해당하는 값을 저장할 배열로, $rows \times cols$ 크기의 2차원 배열로 초기화 후 아래를 수행하여 값을 채워준다.
  - arr의 $i + \frac{j + k}{cols}$ 값을 rows로 나눈 나머지 값의 행, $j + k$를 cols로 나눈 나머지 값의 열에 해당하는 위치에 grid[i][j]의 값을 넣어준다.

3. 결과를 저장할 result를 ArrayList로 초기화 후, arr을 반복하여 순차적으로 값을 채워준다.

4. 각 수행을 통해서 변경된 위치로 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Shift2DGrid.java){:target="_blank"}에서 확인 가능합니다.