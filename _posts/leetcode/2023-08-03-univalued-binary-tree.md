---
title: "Leetcode Java Univalued Binary Tree"
excerpt: "Leetcode Univalued Binary Tree Java"
last_modified_at: 2023-08-03T19:30:00
header:
  image: /assets/images/leetcode/univalued-binary-tree.png
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
[Link](https://leetcode.com/problems/univalued-binary-tree){:target="_blank"}

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

  public boolean isUnivalTree(TreeNode root) {
    return this.isUnivalTree(root.left, root.val) && this.isUnivalTree(root.right, root.val);
  }

  private boolean isUnivalTree(TreeNode root, int value) {
    if (root != null) {
      return root.val == value && this.isUnivalTree(root.left, value) && this.isUnivalTree(root.right, value);
    } else {
      return true;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/univalued-binary-tree/submissions/1011065731/){:target="_blank"}

# 설명
1. 이진 트리인 root를 이용하여 모든 트리의 값이 동일한지 검증하는 문제이다.

2. 3번의 isUnivalTree(TreeNode root, int value) 메서드를 root의 left TreeNode와 val로 수행한 결과와 root의 right TreeNode와 val로 수행한 결과가 모두 충족하는지 여부를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 문제를 풀기 위한 isUnivalTree(TreeNode root, int value) 메서드를 정의한다.
- root가 null이 아니라면 아래 모두 만족하는지 여부를 반환한다.
  - root의 값이 value와 같은 값.
  - root의 left TreeNode를 이용해서 재귀 호출한 결과.
  - root의 right TreeNode를 이용해서 재귀 호출한 결과.
- 위의 경우가 아니라면 노드가 없으므로 true를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UnivaluedBinaryTree.java){:target="_blank"}에서 확인 가능합니다.