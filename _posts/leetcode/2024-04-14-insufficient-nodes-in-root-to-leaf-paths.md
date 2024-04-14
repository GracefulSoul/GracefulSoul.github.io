---
title: "Leetcode Java Insufficient Nodes in Root to Leaf Paths"
excerpt: "Leetcode Insufficient Nodes in Root to Leaf Paths Java"
last_modified_at: 2024-04-14T10:00:00
header:
  image: /assets/images/leetcode/insufficient-nodes-in-root-to-leaf-paths.png
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
[Link](https://leetcode.com/problems/insufficient-nodes-in-root-to-leaf-paths/){:target="_blank"}

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

  public TreeNode sufficientSubset(TreeNode root, int limit) {
    if (root == null) {
      return null;
    } else if (root.left == null && root.right == null) {
      return root.val < limit ? null : root;
    } else {
      root.left = this.sufficientSubset(root.left, limit - root.val);
      root.right = this.sufficientSubset(root.right, limit - root.val);
      return root.left == root.right ? null : root;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/insufficient-nodes-in-root-to-leaf-paths/submissions/1231664484/){:target="_blank"}

# 설명
1. root의 루트 노드부터 리프 노드까지 합계가 limit 이상인 노드가 되기 위해 불필요한 노드들을 삭제하는 문제이다.

2. root 노드가 null인 경우, 그대로 null을 반환한다.

3. root 노드의 left, right 노드가 null인 리프 노드인 경우, root의 val 값이 limit보다 작으면 null을 아니면 root를 반환한다.

4. 그 외의 경우, 아래를 수행한다.
- root의 left와 right TreeNode에 해당 노드와 $limit - root.val$ 값을 이용하여 순차적으로 재귀 호출을 수행한 결과를 넣어준다.
- root의 left와 right가 동일한 null인 경우, null을 아니면 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InsufficientNodesInRootToLeafPaths.java){:target="_blank"}에서 확인 가능합니다.