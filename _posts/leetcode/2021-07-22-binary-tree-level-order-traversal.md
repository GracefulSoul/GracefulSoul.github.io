---
title: "Leetcode Java Binary Tree Level Order Traversal"
excerpt: "Leetcode Binary Tree Level Order Traversal Java 풀이"
last_modified_at: 2021-07-22T17:00:00
header:
  image: /assets/images/leetcode/binary-tree-level-order-traversal.png
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
[Link](https://leetcode.com/problems/binary-tree-level-order-traversal/){:target="_blank"}

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

  public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    this.recursive(root, result, 0);
    return result;
  }

  private void recursive(TreeNode treeNode, List<List<Integer>> result, int level) {
    if (treeNode == null) {
      return;
    }
    if (result.size() < level + 1) {
      result.add(new ArrayList<>());
    }
    result.get(level).add(treeNode.val);
    this.recursive(treeNode.left, result, level + 1);
    this.recursive(treeNode.right, result, level + 1);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/526359175/){:target="_blank"}

# 설명
1. 주어진 TreeNode root를 이용하여 tree의 level 별 val 값들의 집합을 모두 구하는 문제이다.

2. 재귀 호출을 이용하여 root의 각 level 별 val 값들의 집합을 result에 모두 넣어준다.
- treeNode가 null인 경우, TreeNode의 마지막이므로 종료 시킨다.
- result의 size가 $level + 1$보다 작은 경우, level의 처음 값이므로 새로운 ArrayList를 result에 넣어준다.
- result의 level번째 List를 가져와 treeNode의 val 값을 넣어준다.
- left -> right 순으로 값을 넣어주어야 하므로, treeNode의 left TreeNode를 1 증가시킨 level로 재귀 호출을 수행한다.
- 이후 right TreeNode도 1증가시킨 level로 재귀 호출을 수행한다.

3. 재귀 호출이 완료되면 root를 이용하여 level 별 val 값들의 집합으로 구성된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreeLevelOrderTraversal.java){:target="_blank"}에서 확인 가능합니다.