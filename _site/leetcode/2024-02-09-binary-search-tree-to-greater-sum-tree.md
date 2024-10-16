---
title: "Leetcode Java Binary Search Tree to Greater Sum Tree"
excerpt: "Leetcode Binary Search Tree to Greater Sum Tree Java"
last_modified_at: 2024-02-09T14:20:00
header:
  image: /assets/images/leetcode/binary-search-tree-to-greater-sum-tree.png
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
[Link](https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree){:target="_blank"}

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

  public TreeNode bstToGst(TreeNode root) {
    this.bstToGst(root, new TreeNode(0));
    return root;
  }

  private void bstToGst(TreeNode node, TreeNode sum) {
    if (node == null) {
      return;
    }
    this.bstToGst(node.right, sum);
    sum.val += node.val;
    node.val = sum.val;
    this.bstToGst(node.left, sum);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/submissions/1170292312/){:target="_blank"}

# 설명
1. 이진 검색 트리인 root를 이용하여 노드의 값을 현재까지의 모든 값들의 합을 넣은 노드로 변환하는 문제이다.

2. 3번에서 정의한 bstToGst(TreeNode node, TreeNode sum) 메서드를 sum 자리에 새 TreeNode를 넣어 수행한다.

3. 주어진 조건에 맞는 노드의 값을 설정하기 위한 bstToGst(TreeNode node, TreeNode sum) 메서드를 정의한다.
- node가 null인 경우 수행이 불가능하므로, 수행을 중단한다.
- node의 right TreeNode를 이용하여 재귀 호출을 수행한다.
- sum의 val에 node의 val을 더해준 후, node의 val에 sum의 val 값을 넣어준다.
- node의 left TreeNode를 이용하여 재귀 호출을 수행한다.

4. 반복이 완료되면 완성된 root를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinarySearchTreeToGreaterSumTree.java){:target="_blank"}에서 확인 가능합니다.