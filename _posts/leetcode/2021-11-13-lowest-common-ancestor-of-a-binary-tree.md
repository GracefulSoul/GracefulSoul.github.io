---
title: "Leetcode Java Lowest Common Ancestor of a Binary Tree"
excerpt: "Leetcode Lowest Common Ancestor of a Binary Tree Java 풀이"
last_modified_at: 2021-11-13T12:00:00
header:
  image: /assets/images/leetcode/lowest-common-ancestor-of-a-binary-tree.png
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
[Link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) {
      return root;
    } else {
      TreeNode left = lowestCommonAncestor(root.left, p, q);
      TreeNode right = lowestCommonAncestor(root.right, p, q);
      if (left == null) {
        return right;
      } else if (right == null) {
        return left;
      } else {
        return root;
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/586287147/){:target="_blank"}

# 설명
1. 지난번 [Lowest Common Ancestor of a Binary Search Tree](../lowest-common-ancestor-of-a-binary-search-tree){:target="_blank"}와 비슷한 문제로, 주어진 이진 트리인 root에서 TreeNode p와 q의 최소의 공통된 부모 노드인 [LCA](https://en.wikipedia.org/wiki/Lowest_common_ancestor){:target="_blank"}를 찾는 문제이다.

2. root가 null이면 진행이 불가능하고, p와 q 중 하나의 TreeNode가 root와 동일한 경우 최상위인 root가 최소의 공통된 부모 노드이므로 root를 주어진 문제의 결과로 반환한다.

3. 그 외의 경우 root의 left와 right TreeNode를 이용하여 각각 재귀 호출한 결과를 left와 right에 넣어준다.

4. left와 right의 결과에 따라 주어진 문제의 결과를 반환한다.
- left가 null인 경우 left TreeNode를 기준으로 p와 q의 최소의 공통된 부모 노드를 찾지 못했으므로, right를 주어진 문제의 결과로 반환한다.
- right가 null인 경우 right TreeNode를 기준으로 p와 q의 최소의 공통된 부모 노드를 찾지 못했으므로, left를 주어진 문제의 결과로 반환한다.
- left와 right가 둘 다 null인 경우 p와 q의 최소의 공통된 부모 노드가 root밖에 존재하지 않으므로, root를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LowestCommonAncestorOfABinaryTree.java){:target="_blank"}에서 확인 가능합니다.