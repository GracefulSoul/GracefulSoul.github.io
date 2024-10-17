---
title: "Leetcode Java Convert Sorted Array to Binary Search Tree"
excerpt: "Leetcode - 'Convert Sorted Array to Binary Search Tree' 문제 Java 풀이"
last_modified_at: 2021-07-29T12:40:00
header:
  image: /assets/images/leetcode/convert-sorted-array-to-binary-search-tree.png
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
[Link](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/){:target="_blank"}

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

  public TreeNode sortedArrayToBST(int[] nums) {
    return this.recursive(nums, 0, nums.length - 1);
  }

  private TreeNode recursive(int[] nums, int low, int high) {
    if (low > high) {
      return null;
    }
    int mid = (low + high) / 2;
    TreeNode treeNode = new TreeNode(nums[mid]);
    treeNode.left = this.recursive(nums, low, mid - 1);
    treeNode.right = this.recursive(nums, mid + 1, high);
    return treeNode;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/529932117/){:target="_blank"}

# 설명
1. 주어진 정수 배열인 nums를 이용하여 TreeNode를 생성하는 문제이다.

2. 재귀 호출을 이용하여 TreeNode를 만들어 주어진 문제의 결과로 반환한다.
- low가 high보다 큰 경우 nums의 주어진 범위 내에서 TreeNode를 모두 생성한 것이므로, null을 return시킨다.
- 중앙값인 mid를 $\frac{low + high}{2}$의 값을 구해서 TreeNode인 treeNode를 생성한다.
- treeNode의 left에 low부터 $mid - 1$까지 재귀 호출을 수행하여 넣어준다.
- treeNode의 right에 $mid + 1$부터 high까지 재귀 호출을 수행하여 넣어준다.
- 만들어진 treeNode를 반환한다. 최초 재귀 호출의 경우, 주어진 문제로 treeNode를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConvertSortedArrayToBinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.