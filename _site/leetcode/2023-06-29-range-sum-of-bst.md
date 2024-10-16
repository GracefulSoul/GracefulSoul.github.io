---
title: "Leetcode Java Range Sum of BST"
excerpt: "Leetcode Range Sum of BST Java"
last_modified_at: 2023-06-29T19:30:00
header:
  image: /assets/images/leetcode/range-sum-of-bst.png
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
[Link](https://leetcode.com/problems/range-sum-of-bst){:target="_blank"}

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

  public int rangeSumBST(TreeNode root, int low, int high) {
    if (root == null) {
      return 0;
    } else if (root.val > high) {
      return this.rangeSumBST(root.left, low, high);
    } else if (root.val < low) {
      return this.rangeSumBST(root.right, low, high);
    } else {
      return root.val + this.rangeSumBST(root.left, low, high) + this.rangeSumBST(root.right, low, high);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/range-sum-of-bst/submissions/982259826/){:target="_blank"}

# 설명
1. root에서 [low, high] 범위 내 값들의 합을 구하는 문제이다.

2. 아래의각 경우에 따라서 값을 반환한다.
- root가 null인 경우, 값이 없으므로 0을 반환한다.
- root의 val 값이 high보다 큰 경우, 더 작은 값이 존재하는 root의 left TreeNode를 이용하여 재귀 호출을 수행한 결과를 반환한다.
- root의 val 값이 low보다 작은 경우, 더 큰 값이 존재하는 root의 right TreeNode를 이용하여 재귀 호출을 수행한 결과를 반환한다.
- 위의 모든 경우가 아니라면 범위 내 속하는 값이므로, root의 val 값과 left TreeNode를 이용하여 재귀 호출을 수행한 값과 right TreeNode를 이용하여 재귀 호출을 수행한 결과를 합쳐서 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RangeSumOfBST.java){:target="_blank"}에서 확인 가능합니다.