---
title: "Leetcode Java Lowest Common Ancestor of Deepest Leaves"
excerpt: "Leetcode Lowest Common Ancestor of Deepest Leaves Java"
last_modified_at: 2024-06-14T17:50:00
header:
  image: /assets/images/leetcode/lowest-common-ancestor-of-deepest-leaves.png
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
[Link](https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/){:target="_blank"}

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

  private int depth = 0;
  private TreeNode root;

  public TreeNode lcaDeepestLeaves(TreeNode root) {
    this.dfs(root, 0);
    return this.root;
  }

  private int dfs(TreeNode node, int depth) {
    this.depth = Math.max(this.depth, depth);
    if (node == null) {
      return depth;
    } else {
      int left = this.dfs(node.left, depth + 1);
      int right = this.dfs(node.right, depth + 1);
      if (left == this.depth && right == this.depth) {
        this.root = node;
      }
      return Math.max(left, right);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/submissions/1287927384/){:target="_blank"}

# 설명
1. root의 가장 낮은 깊이의 리프 노드들의 공통된 부모 노드를 반환하는 문제이다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- depth는 가장 낮은 깊이를 저장할 변수로, 0으로 초기화한다.
- tree는 가장 낲은 깊이의 리프 노드들의 공통된 부모 노드를 저장할 변수이다.

3. 4번에서 정의한 dfs(TreeNode node, int depth)를 수행한다.

4. DFS 방식으로 가장 낮은 깊이의 리프 노드를 저장하기 위한 dfs(TreeNode node, int depth) 메서드를 정의한다.
- 전역 변수 depth에 해당 값과 현재 깊이인 depth 중 큰 깊이를 저장해준다.
- node가 null인 경우, 현재 depth를 반환한다.
- node가 null이 아닌 경우, 아래를 수행한다.
  - left와 right에 node의 left, right TreeNode와 $depth + 1$을 각각 재귀 호출한 결과를 넣어준다.
  - left와 right의 깊이가 전역 변수인 depth와 동일한 가장 깊은 노드들인 경우, 전역 변수 root에 node를 넣어준다.
  - left와 right 중 큰 깊이를 반환한다.

5. 4번을 통해 가장 깊은 깊이의 노드의 공통된 부모 노드가 저장된 전역 변수인 root의 노드를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LowestCommonAncestorOfDeepestLeaves.java){:target="_blank"}에서 확인 가능합니다.