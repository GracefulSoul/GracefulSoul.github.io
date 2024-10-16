---
title: "Leetcode Java Binary Tree Pruning"
excerpt: "Leetcode Binary Tree Pruning Java"
last_modified_at: 2023-01-23T19:15:00
header:
  image: /assets/images/leetcode/binary-tree-pruning.png
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
[Link](https://leetcode.com/problems/binary-tree-pruning){:target="_blank"}

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

  public TreeNode pruneTree(TreeNode root) {
    if (root == null) {
      return null;
    }
    root.left = this.pruneTree(root.left);
    root.right = this.pruneTree(root.right);
    if (root.left == null && root.right == null && root.val == 0) {
      return null;
    } else {
      return root;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-tree-pruning/submissions/883611179/){:target="_blank"}

# 설명
1. root에서 하위 노드의 합이 1 이상인 노드만 남기는 문제이다.

2. root가 null 인 경우, 존재하지 않는 노드이므로 null을 반환한다.

3. root의 left TreeNode를 재귀 호출한 결과를 해당 TreeNode에, right TreeNode도 동일하게 수행하낟.

4. root의 left와 right TreeNode가 null이면서 val 값은 0이면 null을, 아니면 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreePruning.java){:target="_blank"}에서 확인 가능합니다.