---
title: "Leetcode Java Construct Quad Tree"
excerpt: "Leetcode Construct Quad Tree Java 풀이"
last_modified_at: 2022-03-22T12:00:00
header:
  image: /assets/images/leetcode/construct-quad-tree.png
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
[Link](https://leetcode.com/problems/construct-quad-tree/){:target="_blank"}

# 코드
```java
/*
// Definition for a QuadTree node.
class Node {
    public boolean val;
    public boolean isLeaf;
    public Node topLeft;
    public Node topRight;
    public Node bottomLeft;
    public Node bottomRight;

    
    public Node() {
        this.val = false;
        this.isLeaf = false;
        this.topLeft = null;
        this.topRight = null;
        this.bottomLeft = null;
        this.bottomRight = null;
    }
    
    public Node(boolean val, boolean isLeaf) {
        this.val = val;
        this.isLeaf = isLeaf;
        this.topLeft = null;
        this.topRight = null;
        this.bottomLeft = null;
        this.bottomRight = null;
    }
    
    public Node(boolean val, boolean isLeaf, Node topLeft, Node topRight, Node bottomLeft, Node bottomRight) {
        this.val = val;
        this.isLeaf = isLeaf;
        this.topLeft = topLeft;
        this.topRight = topRight;
        this.bottomLeft = bottomLeft;
        this.bottomRight = bottomRight;
    }
};
*/

class Solution {

  public Node construct(int[][] grid) {
    return this.recursive(grid, 0, grid.length - 1, 0, grid[0].length - 1);
  }

  private Node recursive(int[][] grid, int left, int right, int top, int bottom) {
    if ((left == right && top == bottom) || this.areSameValues(grid, left, right, top, bottom)) {
      return new Node(grid[left][top] == 0 ? false : true, true);
    }
    int rowMid = (left + right) / 2;
    int colMid = (top + bottom) / 2;
    return new Node(false, false,
        this.recursive(grid, left, rowMid, top, colMid),
        this.recursive(grid, left, rowMid, colMid + 1, bottom),
        this.recursive(grid, rowMid + 1, right, top, colMid),
        this.recursive(grid, rowMid + 1, right, colMid + 1, bottom));
  }

  private boolean areSameValues(int[][] grid, int left, int right, int top, int bottom) {
    int value = grid[left][top];
    for (int i = left; i <= right; i++) {
      for (int j = top; j <= bottom; j++) {
        if (grid[i][j] != value) {
          return false;
        }
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/664761906/){:target="_blank"}

# 설명
1. 2차원 정수 배열 grid가 주어지면 해당 배열의 값을 [쿼드 트리](https://en.wikipedia.org/wiki/Quadtree){:target="_blank"}로 표현할 경우의 루트 노드를 반환하는 문제이다.
- 쿼드 트리는 내부에 4개의 하위 트리가 있는 데이터 구조이다.
- val은 노드가 1의 그리드를 나타내면 true이고, 0의 그리드를 나타내면 false로 표현한다.
- isLeaf는 루트 노드인 경우 false이고, 자식 노드인 경우 true로 표현한다.
- 쿼드 트리를 만드는 방법은 간단히 아래와 같다.
  - 전체 영역을 2차원 배열을 4등분 한다.
  - 영역이 동일한 값으로 구성되어 있으면 자식 노드가 없는 노드로 구성한다.
  - 영역이 동일한 값으로 구성되어 있지 않으면 맨 위로 돌아가 해당 영역으로 축소하고 쿼드 트리를 구성한다.

2. 3번에서 정의한 recursive(int[][] grid, int left, int right, int top, int bottom) 메서드를 첫 셀부터 끝 셀까지 위치 값을 넣어 수행한 결과의 노드를 주어진 문제의 결과로 반환한다.

3. 재귀 호출을 활용하여 루트 노드를 만들 recursive(int[][] grid, int left, int right, int top, int bottom) 메서드를 정의한다.
- left와 right가 동일하고 top과 bottom이 동일하거나 4번에서 정의한 areSameValues(int[][] grid, int left, int right, int top, int bottom) 메서드의 결과가 true인 경우 자식 노드이므로, grid[left][top]이 0인지 여부를 val에 isLeaf는 true로 새 Node를 정의하여 반환한다.
- rowMid에 left와 right의 중앙값인 $\frac{left + right}{2}$를, colMid에 top과 bottom의 중앙값인 $\frac{top + bottom}{2}$를 넣어준다.
- 새 노드를 value와 isLeaf를 false로 하고 아래의 각 자식 노드를 넣어 반환한다.
  - topLeft에 right에 rowMid를, bottom에 colMid를 넣어 재귀 호출을 수행한 결과를 넣어준다.
  - topRight에 right에 rowMid를, top에 $colMid + 1$을 넣어 재귀 호출을 수행한 결과를 넣어준다.
  - bottomLeft left에 $rowMid + 1$을, bottom에 colMid를 넣어 재귀 호출을 수행한 결과를 넣어준다.
  - bottomRight left에 $rowMid + 1$을, top에 $colMid + 1$을 넣어 재귀 호출을 수행한 결과를 넣어준다.

4. 특정 구간의 값들이 동일한지를 검증하기 위해 areSameValues(int[][] grid, int left, int right, int top, int bottom) 메서드를 정의한다.
- value에 gird[left][top] 값을 임의 저장하고, 모든 값이 동일하면 ture를 동일하지 않으면 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConstructQuadTree.java){:target="_blank"}에서 확인 가능합니다.