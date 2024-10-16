---
title: "Leetcode Java Find Bottom Left Tree Value"
excerpt: "Leetcode Find Bottom Left Tree Value Java"
last_modified_at: 2022-05-29T06:00:00
header:
  image: /assets/images/leetcode/find-bottom-left-tree-value.png
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
[Link](https://leetcode.com/problems/find-bottom-left-tree-value/){:target="_blank"}

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

  public int findBottomLeftValue(TreeNode root) {
    return this.dfs(root, 1, new int[] { 0, 0 });
  }

  private int dfs(TreeNode root, int depth, int[] result) {
    if (result[1] < depth) {
      result[0] = root.val;
      result[1] = depth;
    }
    if (root.left != null) {
      this.dfs(root.left, depth + 1, result);
    }
    if (root.right != null) {
      this.dfs(root.right, depth + 1, result);
    }
    return result[0];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/709296708/){:target="_blank"}

# 설명
1. root의 왼쪽에 존재하는 모든 노드 중 가장 큰 값을 구하는 문제이다.

2. 3번에서 정의한 dfs(TreeNode root, int depth, int[] result) 메서드를 1 depth부터 result에 [0, 0]를 넣어 수행한 결과를 반환한다.

3. DFS 방식으로 좌측의 모든 노드를 탐색해서 결과를 넣을 dfs(TreeNode root, int depth, int[] result) 메서드를 정의한다.
- depth가 result[1]인 depth가 보다 큰 경우, root의 val 값과 depth를 쌍으로 result에 넣어준다.
- root의 left가 null이 아니면 재귀 호출을 이용하여 depth를 1 증가하여 수행한다.
- root의 right가 null이 아니면 재귀 호출을 이용하여 depth를 1 증가하여 수행한다.
- result[0]인 최대 val 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindBottomLeftTreeValue.java){:target="_blank"}에서 확인 가능합니다.