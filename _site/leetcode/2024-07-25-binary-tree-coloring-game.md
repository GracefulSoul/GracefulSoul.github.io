---
title: "Leetcode Java Binary Tree Coloring Game"
excerpt: "Leetcode Binary Tree Coloring Game Java"
last_modified_at: 2024-07-25T19:40:00
header:
  image: /assets/images/leetcode/binary-tree-coloring-game.png
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
[Link](https://leetcode.com/problems/binary-tree-coloring-game/){:target="_blank"}

# 코드
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

  public boolean btreeGameWinningMove(TreeNode root, int n, int x) {
    if (root == null) {
      return false;
    } else if (root.val == x) {
      int left = this.getCount(root.left);
      int right = this.getCount(root.right);
      int parent = n - (left + right + 1);
      return parent > (left + right) || left > (parent + right) || right > (left + parent);
    } else {
      return this.btreeGameWinningMove(root.left, n, x) || this.btreeGameWinningMove(root.right, n, x);
    }
  }

  private int getCount(TreeNode node) {
    if (node == null) {
      return 0;
    } else {
      return this.getCount(node.left) + this.getCount(node.right) + 1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-tree-coloring-game/submissions/1332868270/){:target="_blank"}

# 설명
1. [1, n]개의 노드가 존재하는 root를 이용하여 아래의 각 턴제 게임을 수행할 때, 이길 수 있는지 검증하는 문제이다.
- 상대 플레이어가 먼저 [1, n] 사이의 노드를 색칠하고, 동일한 노드를 제외한 노드를 색칠한다.
- 각 차례에서 각자 색칠한 노드에서 색칠되지 않은 이웃 노드(자식, 부모 노드) 중 하나를 선택 색칠 하여 더 이상 색칠할 수 없는 노드들이 존재하면, 색칠한 노드가 많으면 게임에서 이긴다.

2. root가 null인 경우, false를 반환한다.

3. 위의 경우가 아니면서, root의 val 값이 x인 경우 아래를 검증한 결과를 반환한다.
- left와 right의 각 노드의 자식 노드들 갯수를 넣어준다.
- parent는 $n - (left + right + 1)$의 결과인 현재 노드 이하를 제외한 잔여 노드의 수를 넣어준다.
- left, right, parent 중 어떤 하나의 값이 다른 두 값보다 큰 이길 가능성이 있으면 true를, 아니면 false를 반환한다.

4. 위의 각 경우가 아니라면 root의 left와 right 노드를 이용하여 재귀 호출한 결과가 하나라도 만족하면 true를, 아니면 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreeColoringGame.java){:target="_blank"}에서 확인 가능합니다.