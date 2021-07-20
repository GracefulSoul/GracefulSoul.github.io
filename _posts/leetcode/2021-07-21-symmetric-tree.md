---
title: "Leetcode Java Symmetric Tree"
excerpt: "Leetcode Symmetric Tree Java 풀이"
last_modified_at: 2021-07-21T08:40:00
header:
  image: /assets/images/leetcode/symmetric-tree.png
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
[Link](https://leetcode.com/problems/symmetric-tree/){:target="_blank"}

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

  public boolean isSymmetric(TreeNode root) {
    return this.recursive(root.left, root.right);
  }

  private boolean recursive(TreeNode p, TreeNode q) {
    if (p == null && q == null) {
      return true;
    } else if (p == null || q == null) {
      return false;
    } else if (p.val == q.val) {
      return this.recursive(p.left, q.right) && this.recursive(p.right, q.left);
    } else {
      return false;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/525723018/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root의 left와 right TreeNode가 대칭이 되는지 검증하는 문제이다.

2. 재귀 호출을 통해 root의 left와 right가 대칭이 되는지 검증하여 결과를 주어진 문제의 결과로 반환한다.
- p와 q가 null인 경우 TreeNode의 끝이 동일하므로, true를 반환한다.
- p가 null이거나 q가 null인 경우 TreeNode의 끝이 다르므로, false를 반환한다.
- p의 val 값과 q의 val 값이 동일하면 재귀 호출을 통해 서로 반대가 되는 p의 left와 q의 right, p의 right와 q의 left TreeNode가 각각 대칭되는 구조인지 다시 검증한 결과의 AND(논리곱) 결과를 반환한다.
- 그 외의 경우는 p와 q의 값이 다른 경우이므로, false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SymmetricTree.java){:target="_blank"}에서 확인 가능합니다.