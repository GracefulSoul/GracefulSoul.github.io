---
title: "Leetcode Java Flatten Binary Tree to Linked List"
excerpt: "Leetcode - 'Flatten Binary Tree to Linked List' 문제 Java 풀이"
last_modified_at: 2021-08-04T12:00:00
header:
  image: /assets/images/leetcode/flatten-binary-tree-to-linked-list.png
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
[Link](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/){:target="_blank"}

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

  public void flatten(TreeNode root) {
    this.recursive(root, null);
  }

  private TreeNode recursive(TreeNode treeNode, TreeNode temp) {
    if (treeNode == null) {
      return temp;
    }
    treeNode.right = this.recursive(treeNode.left, this.recursive(treeNode.right, temp));
    treeNode.left = null;
    return treeNode;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/532960140/){:target="_blank"}

# 설명
1. 주어진 TreeNode의 val 값을 이용하여 우측으로 정렬된 TreeNode로 변경하는 문제이다.

2. 재귀 호출을 이용하여 주어진 TreeNode인 root와 임시 변수인 temp를 이용하여 우측으로 정렬된 TreeNode로 변경하여 주어진 문제를 해결한다.
- treeNode가 null인 경우 마지막 노드이므로, temp를 반환한다.
- treeNode의 right TreeNode에 treeNode의 right TreeNode와 temp로 재귀 호출한 결과를 다시 treeNode의 left TreeNode와 재귀 호출한 결과를 넣어준다.
- TreeNode의 left TreeNode는 값을 제거해야 하므로, null을 넣어준다.
- 위의 단계를 수행하고 treeNode를 반환해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlattenBinaryTreeToLinkedList.java){:target="_blank"}에서 확인 가능합니다.