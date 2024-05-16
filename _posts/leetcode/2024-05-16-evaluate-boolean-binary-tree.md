---
title: "Leetcode Java Evaluate Boolean Binary Tree"
excerpt: "Leetcode Evaluate Boolean Binary Tree Java"
last_modified_at: 2024-05-16T17:00:00
header:
  image: /assets/images/leetcode/evaluate-boolean-binary-tree.png
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
[Link](https://leetcode.com/problems/evaluate-boolean-binary-tree/){:target="_blank"}

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

  public boolean evaluateTree(TreeNode root) {
    if (root.left == null && root.right == null) {
      return root.val == 1;
    } else {
      boolean left = this.evaluateTree(root.left);
      boolean right = this.evaluateTree(root.right);
      return root.val == 2 ? left || right : left && right;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/path-with-maximum-gold/submissions/1257820418/){:target="_blank"}

# 설명
1. 아래의 규칙에 해당하는 값이 들어가있는 TreeNode인 root를 이용하여 최종 결과를 계산하여 반환하는 문제이다.
- 자식 노드가 없는 리프 노드는 0인 False와 1인 True의 값을 가진다.
- 자식 노드가 존재하는 노드는 2인 OR 논리 연산식과 3인 AND 논리 연산식을 가지며, 자식 노드의 연산 결과를 값으로 가진다.

2. root의 자식 노드가 없는 경우, root가 1인 true인지 검증한 결과를 반환한다.

3. root의 자식 노드가 있는 경우, 아래를 수행한다.
- left와 right에 root의 left와 right TreeNode를 이용하여 각각 재귀 호출한 결과를 넣어준다.
- root의 val 값이 2인 OR 연산인 경우, left || right의 OR 연산 결과를 아니면 left && right의 AND 연산 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PathWithMaximumGold.java){:target="_blank"}에서 확인 가능합니다.