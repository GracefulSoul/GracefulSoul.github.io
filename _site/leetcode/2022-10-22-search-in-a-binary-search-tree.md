---
title: "Leetcode Java Search in a Binary Search Tree"
excerpt: "Leetcode Search in a Binary Search Tree Java"
last_modified_at: 2022-10-22T09:00:00
header:
  image: /assets/images/leetcode/search-in-a-binary-search-tree.png
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
[Link](https://leetcode.com/problems/search-in-a-binary-search-tree){:target="_blank"}

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

  public TreeNode searchBST(TreeNode root, int val) {
    while (root != null && root.val != val) {
      root = val < root.val ? root.left : root.right;
    }
    return root;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/827626066/){:target="_blank"}

# 설명
1. 이진 탐색 트리인 root 내 val 값인 노드를 찾는 문제이다.

2. root가 null이 아니면서 root의 val 값이 val과 다른 경우, 계속 반복하여 아래의 경우에 따라 탐색을 수행한다.
- val의 값이 root의 val 값보다 작은 경우, val 값이 root의 left TreeNode의 val 값에 가까우므로 root에 left TreeNode를 넣어준다.
- 위의 경우가 아닌 경우, val 값이 root의 right TreeNode의 val 값에 가까우므로 root에 right TreeNode를 넣어준다.

3. 반복이 완료되면 탐색된 노드인 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SearchInABinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.