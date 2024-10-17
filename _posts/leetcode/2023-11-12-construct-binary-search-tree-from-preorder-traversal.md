---
title: "Leetcode Java Construct Binary Search Tree from Preorder Traversal"
excerpt: "Leetcode Medium - 'Construct Binary Search Tree from Preorder Traversal' 문제 Java 풀이"
last_modified_at: 2023-11-12T13:00:00
header:
  image: /assets/images/leetcode/construct-binary-search-tree-from-preorder-traversal.png
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
[Link](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal){:target="_blank"}

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

  public TreeNode bstFromPreorder(int[] preorder) {
    return this.bst(preorder, Integer.MAX_VALUE, new int[] { 0 });
  }

  private TreeNode bst(int[] preorder, int bound, int[] i) {
    if (i[0] == preorder.length || bound < preorder[i[0]]) {
      return null;
    }
    TreeNode root = new TreeNode(preorder[i[0]++]);
    root.left = this.bst(preorder, root.val, i);
    root.right = this.bst(preorder, bound, i);
    return root;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/submissions/1097021993/){:target="_blank"}

# 설명
1. preorder를 이용하여 Pre-Order의 TreeNode를 완성하는 문제이다.

2. BST로 TreeNode를 완성할 bstFromPreorder(int[] preorder, int bound, int[] i) 메서드를 수행하여 만들어진 TreeNode를 주어진 문제의 결과로 반환한다.
- i[0]이 preorder의 길이와 동일하거나 bound가 preorder[i[0]] 값보다 작은 경우, 노드를 만들 수 없으므로 null을 반환한다.
- root에 preorder[i[0]] 값을 가진 TreeNode를 만들어주고 i[0] 값을 증가시킨다.
- root의 left TreeNode 위치에 root의 val 값을 이용한 재귀 호출을 수행한 결과를 넣어준다.
- root의 right TreeNode 위치에 bound 값을 이용한 재귀 호출을 수행한 결과를 넣어준다.
- 수행이 완료되면 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignGraphWithShortestPathCalculator.java){:target="_blank"}에서 확인 가능합니다.