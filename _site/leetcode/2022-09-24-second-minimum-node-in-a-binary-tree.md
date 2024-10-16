---
title: "Leetcode Java Maximum Swap"
excerpt: "Leetcode Maximum Swap Java"
last_modified_at: 2022-09-23T19:30:00
header:
  image: /assets/images/leetcode/second-minimum-node-in-a-binary-tree.png
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
[Link](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree){:target="_blank"}

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

  public int findSecondMinimumValue(TreeNode root) {
    return this.dfs(root, root.val);
  }

  private int dfs(TreeNode root, int min) {
    if (root == null) {
      return -1;
    } else if (root.val > min) {
      return root.val;
    } else {
      int left = this.dfs(root.left, min);
      int right = this.dfs(root.right, min);
      return left == -1 || right == -1 ? Math.max(left, right) : Math.min(left, right);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/807186221/){:target="_blank"}

# 설명
1. root의 모든 TreeNode의 두 번째로 작은 값을 찾는 문제이다.
- 단, 두 번째로 작은 값이 없으면 -1을 반환한다.

2. 3번에서 정의한 dfs(TreeNode root, int min) 메서드에 root와 root의 val 값을 이용하여 탐색된 값을 주어진 문제의 결과로 반환한다.

3. 두 번째로 작은 값을 찾기 위한 dfs(TreeNode root, int min) 메서드를 정의한다.
- root가 null인 경우 탐색이 불가능하므로, -1을 반환한다.
- 위의 경우가 아니면서 root의 val 값이 min보다 큰 경우 최소 값보다 크므로, root의 val 값을 반환한다.
- 위의 경우들이 아니면 아래를 수행한다.
  - left에 root의 left TreeNode와 min을 이용하여 재귀 호출을 수행한 결과를 넣어준다.
  - right에 root의 right TreeNode와 min을 이용하여 재귀 호출을 수행한 결과를 넣어준다.
  - left가 -1이거나 right가 -1인 경우 두 노드 중 존재하지 않는 노드가 있으므로, left와 right 중 큰 값을, 아니면 left와 right 중 작은 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SecondMinimumNodeInABinaryTree.java){:target="_blank"}에서 확인 가능합니다.