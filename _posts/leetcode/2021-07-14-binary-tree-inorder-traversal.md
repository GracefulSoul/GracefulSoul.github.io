---
title: "Leetcode Java Binary Tree Inorder Traversal"
excerpt: "Leetcode - 'Binary Tree Inorder Traversal' 문제 Java 풀이"
last_modified_at: 2021-07-14T13:00:00
header:
  image: /assets/images/leetcode/binary-tree-inorder-traversal.png
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
[Link](https://leetcode.com/problems/binary-tree-inorder-traversal/){:target="_blank"}

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

  public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    this.recursive(result, root);
    return result;
  }

  private void recursive(List<Integer> result, TreeNode node) {
    if (node != null) {
      this.recursive(result, node.left);
      result.add(node.val);
      this.recursive(result, node.right);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/522184336/){:target="_blank"}

# 설명
1. [이진 트리](https://en.wikipedia.org/wiki/Binary_tree){:target="_blank"}로 구성된 TreeNode를 전달하면, 각 노드 기준으로 좌측 자식 노드 -> 루트 노드 -> 우측 자식 노드 순으로 숫자를 나열하는 문제이다.

2. 주어진 TreeNode인 root를 기준으로 재귀 호출을 통해 각 숫자들을 result에 넣어준다.
- node가 null이 아닌 경우, 노드가 존재하므로 아래의 순서대로 순차 실행을 한다.
  - 좌측 자식 노드인 node.left를 node자리에 넣어 재귀 호출을 수행한다.
  - result에 node의 val 값을 넣어준다.
  - 우측 자식 노드인 node.right를 node 자리에 넣어 재귀 호출을 수행한다.

3. 재귀 호출이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreeInorderTraversal.java){:target="_blank"}에서 확인 가능합니다.