---
title: "Leetcode Java Validate Binary Search Tree"
excerpt: "Leetcode Validate Binary Search Tree Java 풀이"
last_modified_at: 2021-07-18T14:40:00
header:
  image: /assets/images/leetcode/validate-binary-search-tree.png
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
[Link](https://leetcode.com/problems/validate-binary-search-tree/){:target="_blank"}

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

  public boolean isValidBST(TreeNode root) {
    return this.recursive(root, null, null);
  }

  private boolean recursive(TreeNode root, Integer min, Integer max) {
    if (root == null) {
      return true;
    } else if ((min != null && root.val <= min) || (max != null && root.val >= max)) {
      return false;
    } else {
      return this.recursive(root.left, min, root.val) && this.recursive(root.right, root.val, max);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/524270998/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root가 유효한 [이진 검색 트리](https://en.wikipedia.org/wiki/Binary_search_tree){:target="_blank"}인지 검증하는 문제이다.
- 이진 검색 트리의 조건은 아래와 같다.
  - 노드의 왼쪽 아래 구성되는 노드의 값은 상위 노드의 값보다 작은 값이어야 한다.
  - 노드의 오른쪽 아래 구성되는 노드의 값은 상위 노드의 값보다 큰 값이어야 한다.
  - 루트 이하 모든 노드들은 위의 두 조건을 따른다.

2. 재귀 호출을 이용하여 min 값과 max 값을 이용하여 이진 검색 트리가 유효한지 검증한다.
- root가 null인 경우 왼쪽 아래와 오른쪽 아래 노드가 없어 검증의 의미가 없으므로, true를 반환한다.
- 아래의 조건에 일치하면 이진 검색 트리 조건에 부합하지 않으므로, false를 반환한다.
  - min이 null이 아니고 root의 val 값이 min보다 작거나 같다.
  - max가 null이 아니고 root의 val 값이 max보다 크거나 같다.
- 그 외의 경우 root의 왼쪽 아래 구성되는 노드가 유효한지와 오른쪽 아래 구성되는 노드 기준의 검증 결과가 유효한지 검증하여 AND(논리곱)으로 연산한 결과를 반환한다.
- 최종 검증이 끝난 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidateBinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.