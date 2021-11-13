---
title: "Leetcode Java Lowest Common Ancestor of a Binary Search Tree"
excerpt: "Leetcode Lowest Common Ancestor of a Binary Search Tree Java 풀이"
last_modified_at: 2021-11-12T12:00:00
header:
  image: /assets/images/leetcode/lowest-common-ancestor-of-a-binary-search-tree.png
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
[Link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    while ((root.val - p.val) * (root.val - q.val) > 0) {
      root = root.val > p.val ? root.left : root.right;
    }
    return root;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/585843867/){:target="_blank"}

# 설명
1. 주어진 이진 탐색 트리([BST](https://en.wikipedia.org/wiki/Binary_search_tree){:target="_blank"})인 root에서 TreeNode p와 q의 최소의 공통된 부모 노드인 [LCA](https://en.wikipedia.org/wiki/Lowest_common_ancestor){:target="_blank"}를 찾는 문제이다.

2. 주어진 TreeNode인 root의 val 값에 p의 val 값을 뺀 값과 root의 val 값에 q의 val 값을 뺀 값이 0보다 큰 경우 root의 노드가 해당 노드보다 큰 val 값을 가진 경우이므로, 아래를 수행하고 반복을 계속 수행한다.
- root의 val 값이 p의 val 값보다 큰 경우, root의 left TreeNode를 root에 넣어준다.
- root의 val 값이 p의 val 값보다 같거나 작은 경우, root의 right TreeNode를 root에 넣어준다.

3. 반복이 완료되면 최소의 공통된 부모 노드를 저정한 root를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LowestCommonAncestorOfABinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.