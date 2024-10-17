---
title: "Leetcode Java Binary Tree Postorder Traversal"
excerpt: "Leetcode - 'Binary Tree Postorder Traversal' 문제 Java 풀이"
last_modified_at: 2021-09-03T09:00:00
header:
  image: /assets/images/leetcode/binary-tree-postorder-traversal.png
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
[Link](https://leetcode.com/problems/binary-tree-postorder-traversal/){:target="_blank"}

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

  public List<Integer> postorderTraversal(TreeNode root) {
    return this.recursive(root, new ArrayList<>());
  }

  private List<Integer> recursive(TreeNode treeNode, List<Integer> list) {
    if (treeNode != null) {
      this.recursive(treeNode.left, list);
      this.recursive(treeNode.right, list);
      list.add(treeNode.val);
    }
    return list;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/548623955/){:target="_blank"}

# 설명
1. preorder 순으로 주어진 TreeNode인 root의 하위 ListNode val 값을 List에 넣는 문제이다.
- preorder는 left -> right -> root 순이다.

2. 재귀 호출을 이용하여 List에 preorder 순으로 val 값들을 넣어 주어진 문제의 결과로 반환한다.
- treeNode가 null이 아닌 경우 존재하는 TreeNode이므로 아래를 수행한다.
  - treeNode.left를 재귀 호출 수행하여 treeNode의 left TreeNode 하위 val 값을 list에 넣어준다.
  - treeNode.right를 재귀 호출 수행하여 treeNode의 right TreeNode 하위 val 값을 list에 넣어준다.
  - list에 treeNode.val 값을 넣어준다.
- list를 반환하여 계속 list에 TreeNode의 val 값을 preorder 순으로 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreePostorderTraversal.java){:target="_blank"}에서 확인 가능합니다.