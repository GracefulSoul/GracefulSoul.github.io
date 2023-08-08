---
title: "Leetcode Java Flip Binary Tree To Match Preorder Traversal"
excerpt: "Leetcode Flip Binary Tree To Match Preorder Traversal Java"
last_modified_at: 2023-08-08T18:50:00
header:
  image: /assets/images/leetcode/flip-binary-tree-to-match-preorder-traversal.png
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
[Link](https://leetcode.com/problems/flip-binary-tree-to-match-preorder-traversal){:target="_blank"}

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

  private int index;

  public List<Integer> flipMatchVoyage(TreeNode root, int[] voyage) {
    this.index = 0;
    List<Integer> result = new ArrayList<>();
    return this.dfs(root, voyage, result) ? result : Arrays.asList(-1);
  }

  private boolean dfs(TreeNode node, int[] voyage, List<Integer> result) {
    if (node == null) {
      return true;
    } else if (node.val != voyage[index++]) {
      return false;
    } else if (node.left != null && node.left.val != voyage[index]) {
      result.add(node.val);
      return this.dfs(node.right, voyage, result) && this.dfs(node.left, voyage, result);
    } else {
      return this.dfs(node.left, voyage, result) && this.dfs(node.right, voyage, result);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/flip-binary-tree-to-match-preorder-traversal/submissions/1015535309/){:target="_blank"}

# 설명
1. root를 자식 노드의 순서만 바꾸며 Preorder로 voyage와 비교할 때, 변경한 노드의 값들을 반환하는 문제이다.
- 단, Preorder 구성이 불가능한 경우에는 -1을 넣어 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- 전역 변수인 index는 voyage 내 위치를 저장할 변수로, 0으로 초기화한다.
- result는 변경하는 노드의 값을 저장할 변수로, ArrayList로 초기화한다.

3. 4번에서 정의한 dfs(TreeNode node, int[] voyage, List<Integer> result) 메서드를 수행한 결과가 true이면 result를, 아니면 -1을 List로 변환하여 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 root를 탐색할 dfs(TreeNode node, int[] voyage, List<Integer> result) 메서드를 정의한다.
- node가 null인 경우, true를 반환한다.
- node의 값이 voyage의 index번째 값과 동일하지 않으면 일치하지 않으므로, false를 반환하고 결과와 무관하게 index를 증가시킨다.
- node의 left TreeNode가 null이 아니면서 val 값이 voyage의 index번째 노드와 같지 않은 경우, 아래를 수행한다.
  - result에 node의 val 값을 넣고, node의 right TreeNode로 재귀 호출을 수행한 결과와 left TreeNode로 재귀 호출을 수행한 결과의 AND 연산을 수행한 값을 반환한다.
- 위의 모든 경우가 아니라면 node의 left TreeNode로 재귀 호출을 수행한 결과와 right TreeNode로 재귀 호출을 수행한 결과의 AND 연산을 수행한 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlipBinaryTreeToMatchPreorderTraversal.java){:target="_blank"}에서 확인 가능합니다.