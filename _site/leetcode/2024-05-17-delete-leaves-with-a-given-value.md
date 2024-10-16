---
title: "Leetcode Java Delete Leaves With a Given Value"
excerpt: "Leetcode Delete Leaves With a Given Value Java"
last_modified_at: 2024-05-17T20:00:00
header:
  image: /assets/images/leetcode/delete-leaves-with-a-given-value.png
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
[Link](https://leetcode.com/problems/delete-leaves-with-a-given-value/){:target="_blank"}

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

  public TreeNode removeLeafNodes(TreeNode root, int target) {
    if (root.left != null) {
      root.left = this.removeLeafNodes(root.left, target);
    }
    if (root.right != null) {
      root.right = this.removeLeafNodes(root.right, target);
    }
    return root.left == root.right && root.val == target ? null : root;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/delete-leaves-with-a-given-value/submissions/1260447191/){:target="_blank"}

# 설명
1. root 내 target이 val로 가진 리프 노드를 삭제하는 문제이다.

2. root의 left TreeNode가 존재하는 경우, root의 left TreeNode로 재귀 호출을 수행한 결과를 해당 자리에 넣어준다.

3. root의 right TreeNode가 존재하는 경우 위와 동일하게, root의 right TreeNode로 재귀 호출을 수행한 결과를 해당 자리에 넣어준다.

4. root의 left와 right TreeNode가 동일하게 null이면서 root의 val 값이 target인 경우 null을, 아니면 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PathWithMaximumGold.java){:target="_blank"}에서 확인 가능합니다.