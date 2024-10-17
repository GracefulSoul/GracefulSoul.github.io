---
title: "Leetcode Java Insert into a Binary Search Tree"
excerpt: "Leetcode - 'Insert into a Binary Search Tree' 문제 Java 풀이"
last_modified_at: 2022-10-23T17:50:00
header:
  image: /assets/images/leetcode/insert-into-a-binary-search-tree.png
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
[Link](https://leetcode.com/problems/insert-into-a-binary-search-tree){:target="_blank"}

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

  public TreeNode insertIntoBST(TreeNode root, int val) {
    if (root == null) {
      return new TreeNode(val);
    } else if (root.val > val) {
      root.left = this.insertIntoBST(root.left, val);
    } else {
      root.right = this.insertIntoBST(root.right, val);
    }
    return root;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/828508648/){:target="_blank"}

# 설명
1. 이진 탐색 트리인 root 내 val 값인 노드를 추가하는 문제이다.

2. root가 null이면, 해당 자리에 노드를 추가하면 되므로 새 TreeNode를 val 값으로 초기화하여 반환한다.

3. 아래의 경우에 따라 수행하여 val 값의 노드를 추가한 root를 주어진 문제의 결과로 반환한다.
- root의 val 값이 val보다 큰 경우 좌측 자식 노드 방향으로 탐색해야하므로, root의 left TreeNode에 root의 left TreeNode로 재귀 호출한 결과를 넣어준다.
- root의 val 값이 val보다 작거나 같은 경우 우측 자식 노드 방향으로 탐색해야하므로, root의 right TreeNode에 root의 right TreeNode로 재귀 호출한 결과를 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SearchInABinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.