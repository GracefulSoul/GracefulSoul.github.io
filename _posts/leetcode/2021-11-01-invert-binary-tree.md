---
title: "Leetcode Java Invert Binary Tree"
excerpt: "Leetcode Invert Binary Tree Java 풀이"
last_modified_at: 2021-11-01T13:00:00
header:
  image: /assets/images/leetcode/invert-binary-tree.png
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
[Link](https://leetcode.com/problems/invert-binary-tree/){:target="_blank"}

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

  public TreeNode invertTree(TreeNode root) {
    if (root == null) {
      return null;
    } else if (root.left != null || root.right != null) {
      TreeNode left = root.left;
      root.left = this.invertTree(root.right);
      root.right = this.invertTree(left);
    }
    return root;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/580299155/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root의 자식 노드들의 좌우 위치를 반대로 바꾸어 주는 문제이다.

2. root가 null인 경우 끝 노드이므로, null을 반환한다.

3. root의 left 혹은 right 자식 노드가 존재하는 경우, 아래를 수행하여 좌우 위치를 반대로 바꾸어 준다.
- 임시 변수인 left를 정의하여 root.left TreeNode를 넣어준다.
- root.left에 root.right를 이용하여 재귀 호출을 수행한 결과를 넣어준다.
- root.right에 left를 이용하여 재귀 호출을 수행한 결과를 넣어준다.

4. 자식 노드들의 좌우 위치를 반대로 바꾼 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InvertBinaryTree.java){:target="_blank"}에서 확인 가능합니다.