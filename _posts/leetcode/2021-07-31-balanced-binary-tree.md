---
title: "Leetcode Java Balanced Binary Tree"
excerpt: "Leetcode Balanced Binary Tree Java 풀이"
last_modified_at: 2021-07-31T15:50:00
header:
  image: /assets/images/leetcode/balanced-binary-tree.png
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
[Link](https://leetcode.com/problems/balanced-binary-tree/){:target="_blank"}

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

  public boolean isBalanced(TreeNode root) {
    return this.recursive(root) != -1;
  }

  private int recursive(TreeNode root) {
    if (root == null) {
      return 0;
    }
    int left = this.recursive(root.left);
    int right = this.recursive(root.right);
    if (left == -1 || right == -1 || Math.abs(left - right) > 1) {
      return -1;
    } else {
      return Math.max(left, right) + 1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/530932178/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root가 균형을 이루고 있는지를 검증하는 문제이다.

2. 재귀 호출을 이용하여 root가 균형을 이루고 있는지 검증한다.
- root가 null인 경우 마지막 노드이므로, 0을 반환한다.
- left를 root의 left TreeNode의 재귀 호출 결과로 정의한다.
- right를 root의 right TreeNode의 재귀 호출 결과로 정의한다.
- left와 right가 -1이거나, $left - right$의 절대값이 1 초과인 경우 불균형을 이루므로, -1을 반환한다.
- 위의 경우가 아닌 경우 left와 rigth의 최대 값에 1을 더하여 반환한다.

3. 재귀 호출읠 결과가 -1이 아니면 균형을 이루고 있으므로 true를, -1이면 균형을 이루고 있지 않으므로 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BalancedBinaryTree.java){:target="_blank"}에서 확인 가능합니다.