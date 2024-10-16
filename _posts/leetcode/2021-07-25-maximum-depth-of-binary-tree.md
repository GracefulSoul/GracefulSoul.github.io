---
title: "Leetcode Java Maximum Depth of Binary Tree"
excerpt: "Leetcode Maximum Depth of Binary Tree Java 풀이"
last_modified_at: 2021-07-25T10:00:00
header:
  image: /assets/images/leetcode/maximum-depth-of-binary-tree.png
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
[Link](https://leetcode.com/problems/maximum-depth-of-binary-tree/){:target="_blank"}

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

  public int maxDepth(TreeNode root) {
    return this.recursive(root, 0);
  }

  private int recursive(TreeNode treeNode, int depth) {
    if (treeNode == null) {
      return depth;
    } else {
      return Math.max(this.recursive(treeNode.left, depth + 1), this.recursive(treeNode.right, depth + 1));
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/527787818/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root의 최대 깊이를 구하는 문제이다.

2. 재귀 호출을 통해서 root의 최대 깊이를 구하여 주어진 문제의 결과로 반환한다.
- treeNode가 null인 경우 해당 노드의 마지막이므로, depth를 반환한다.
- 그 외의 경우에는 treeNode의 left와 right를 각각 $depth + 1$로 재귀호출을 수행한 결과 중 가장 큰 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumDepthOfBinaryTree.java){:target="_blank"}에서 확인 가능합니다.