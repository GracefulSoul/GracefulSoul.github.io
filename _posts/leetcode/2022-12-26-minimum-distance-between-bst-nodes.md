---
title: "Leetcode Java Minimum Distance Between BST Nodes"
excerpt: "Leetcode - 'Minimum Distance Between BST Nodes' 문제 Java 풀이"
last_modified_at: 2022-12-26T13:55:00
header:
  image: /assets/images/leetcode/minimum-distance-between-bst-nodes.png
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
[Link](https://leetcode.com/problems/minimum-distance-between-bst-nodes){:target="_blank"}

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

  private int min = Integer.MAX_VALUE;
  private int pre = -1;

  public int minDiffInBST(TreeNode root) {
    if (root.left != null) {
      this.minDiffInBST(root.left);
    }
    if (this.pre != -1) {
      this.min = Math.min(this.min, root.val - this.pre);
    }
    this.pre = root.val;
    if (root.right != null) {
      this.minDiffInBST(root.right);
    }
    return this.min;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-distance-between-bst-nodes/submissions/865549066/){:target="_blank"}

# 설명
1. 이진 탐색 트리(BST)인 root를 이용하여 인접한 두 노드 간 값의 차이가 가장 작은 값을 구하는 문제이다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- min은 최솟값을 저장하기 위한 변수로, 정수의 가장 큰 값을 넣어준다.
- pre는 이전 값을 임시 저장할 변수로, val 값의 범위에 존재하지 않는 -1로 초기화한다.

3. root의 left TreeNode가 null이 아닌 경우, root의 left TreeNode를 이용하여 재귀 호출을 수행한다.

4. pre의 값이 -1이 아닌 경우, min에 min과 root의 val 값과 pre의 차이 중 작은 값을 저장한다.

5. pre에 root의 val 값을 넣어 값을 임시 저장한다.

6. root의 right TreeNode가 null이 아닌 경우, root의 right TreeNode를 이용하여 재귀 호출을 수행한다.

7. 반복이 완료되면 인접한 두 노드 간 값의 차이가 가장 작은 값을 저장한 min을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumDistanceBetweenBSTNodes.java){:target="_blank"}에서 확인 가능합니다.