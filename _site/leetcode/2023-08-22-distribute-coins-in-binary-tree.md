---
title: "Leetcode Java Distribute Coins in Binary Tree"
excerpt: "Leetcode Distribute Coins in Binary Tree Java"
last_modified_at: 2023-08-22T18:55:00
header:
  image: /assets/images/leetcode/distribute-coins-in-binary-tree.png
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
[Link](https://leetcode.com/problems/distribute-coins-in-binary-tree){:target="_blank"}

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

  private int result;

  public int distributeCoins(TreeNode root) {
    this.result = 0;
    this.dfs(root);
    return this.result;
  }

  private int dfs(TreeNode root) {
    if (root == null) {
      return 0;
    } else {
      int left = this.dfs(root.left);
      int right = this.dfs(root.right);
      this.result += Math.abs(left) + Math.abs(right);
      return root.val + left + right - 1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/distribute-coins-in-binary-tree/submissions/1028463957/){:target="_blank"}

# 설명
1. root 내 모든 노드들이 정확히 하나의 val 값을 가지도록 분배하는데 소모되는 횟수를 구하는 문제이다.
- 한 번에 인접한 한 노드로 코인을 이동할 수 있다.

2. result는 횟수를 구하기 위한 변수이다.

3. result를 0으로 초기화하고 4번에서 정의한 dfs(TreeNode root) 메서드를 수행한다.

4. DFS 방식으로 이동 횟수를 계산할 dfs(TreeNode root) 메서드를 정의한다.
- root가 null인 경우, 이동이 불가능하므로 0을 반환한다.
- 그 외의 경우 아래를 수행한다.
  - left에 root의 left TreeNode를 이용하여 수행한 결과를 넣어준다.
  - right에 root의 right TreeNode를 이용하여 수행한 결과를 넣어준다.
  - result에 left와 right의 절댓값을 더한 값을 더해 이동 횟수를 계산한다.
  - root의 val 값과 left, right를 더한 후 이동횟수인 1을 뺀 값을 반환한다.

5. 4번의 수행이 완료되면 이동 횟수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DistributeCoinsInBinaryTree.java){:target="_blank"}에서 확인 가능합니다.