---
title: "Leetcode Java Binary Tree Zigzag Level Order Traversal"
excerpt: "Leetcode Binary Tree Zigzag Level Order Traversal Java 풀이"
last_modified_at: 2021-07-23T08:40:00
header:
  image: /assets/images/leetcode/binary-tree-zigzag-level-order-traversal.png
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
[Link](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/){:target="_blank"}

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

  public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
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
    if (level % 2 == 0) {
      result.get(level).add(treeNode.val);
    } else {
      result.get(level).add(0, treeNode.val);
    }
    this.recursive(treeNode.left, result, level + 1);
    this.recursive(treeNode.right, result, level + 1);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/526784911/){:target="_blank"}

# 설명
1. 주어진 TreeNode root를 이용하여 tree의 level 별 val 값들의 집합을 모두 구하는 문제이다. 단, 짝수 번째 level의 경우 역순으로(right -> left) val 값들의 집합으로 구성해야 한다.

2. 이전의 [Binary Tree Level Order Traversal](../binary-tree-level-order-traversal)과 유사한 문제이다.
- 단, 기존의 경우 모든 부분 집합의 정렬 순서가 left -> right였다.
- 변경된 룰은 홀수 번째 level의 경우 부분 집합의 정렬 순서는 left -> right이고, 짝수 번째 level의 경우 부분 집합이의 정렬 순서는 right -> left이다.

3. 재귀 호출을 이용하여 root의 각 level 별 val 값들의 집합을 result에 모두 넣어준다.
- treeNode가 null인 경우, TreeNode의 마지막이므로 종료 시킨다.
- result의 size가 $level + 1$보다 작은 경우, level의 처음 값이므로 새로운 ArrayList를 result에 넣어준다.
- 순차적으로 result의 level번째 List를 가져와 treeNode의 val 값을 넣어준다.
  - $level \mod 2$로 짝수인 경우, List의 뒤에 순차적으로 val 값을 넣어준다.
  - $level \mod 2$로 홀수인 경우, List의 앞에 역순으로 val 값을 넣어준다.
- left -> right 순으로 값을 넣어주어야 하므로, treeNode의 left TreeNode를 1 증가시킨 level로 재귀 호출을 수행한다.
- 이후 right TreeNode도 1증가시킨 level로 재귀 호출을 수행한다.

3. 재귀 호출이 완료되면 root를 이용하여 level 별 val 값들의 집합으로 구성된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreeZigzagLevelOrderTraversal.java){:target="_blank"}에서 확인 가능합니다.