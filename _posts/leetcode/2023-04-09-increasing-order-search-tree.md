---
title: "Leetcode Java Increasing Order Search Tree"
excerpt: "Leetcode - 'Increasing Order Search Tree' 문제 Java 풀이"
last_modified_at: 2023-04-09T10:10:00
header:
  image: /assets/images/leetcode/increasing-order-search-tree.png
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
[Link](https://leetcode.com/problems/increasing-order-search-tree){:target="_blank"}

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

  public TreeNode increasingBST(TreeNode root) {
    return this.dfs(root, null);
  }

  private TreeNode dfs(TreeNode root, TreeNode tail) {
    if (root == null) {
      return tail;
    } else {
      TreeNode temp = this.dfs(root.left, root);
      root.left = null;
      root.right = this.dfs(root.right, tail);
      return temp;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/increasing-order-search-tree/submissions/930393509/){:target="_blank"}

# 설명
1. 이진 트리 노드인 root를 이용하여 우측 자식 노드로 값이 증가하는 TreeNode를 만드는 문제이다.

2. 3번에서 정의한 dfs 메서드에 root와 null을 넣고 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 TreeNode를 만들 dfs(TreeNode root, TreeNode tail) 메서드를 정의한다.
- root가 null인 경우, tail을 반환한다.
- root가 null이 아니면 아래를 수행한다.
  - temp에 root의 left TreeNode와 root를 이용한 재귀 호출 결과를 넣어준다.
  - temp의 left TreeNode에 null을 넣고, right TreeNode에 root의 right TreeNode와 tail을 이용한 재귀 호출 결과를 넣어준다.
  - 만들어진 TreeNode인 temp를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IncreasingOrderSearchTree.java){:target="_blank"}에서 확인 가능합니다.