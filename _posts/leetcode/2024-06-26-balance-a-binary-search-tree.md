---
title: "Leetcode Java Balance a Binary Search Tree"
excerpt: "Leetcode Medium - 'Balance a Binary Search Tree Square' 문제 Java 풀이"
last_modified_at: 2024-06-26T18:30:00
header:
  image: /assets/images/leetcode/balance-a-binary-search-tree.png
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
[Link](https://leetcode.com/problems/balance-a-binary-search-tree/){:target="_blank"}

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

  public TreeNode balanceBST(TreeNode root) {
    List<TreeNode> list = new ArrayList<>();
    this.addListInorder(root, list);
    return this.createBalanceBST(list, 0, list.size() - 1);
  }

  private void addListInorder(TreeNode root, List<TreeNode> list) {
    if (root != null) {
      this.addListInorder(root.left, list);
      list.add(root);
      this.addListInorder(root.right, list);
    }
  }

  private TreeNode createBalanceBST(List<TreeNode> list, int start, int end) {
    if (start > end) {
      return null;
    } else {
      int mid = (start + end) / 2;
      TreeNode root = list.get(mid);
      root.left = this.createBalanceBST(list, start, mid - 1);
      root.right = this.createBalanceBST(list, mid + 1, end);
      return root;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/balance-a-binary-search-tree/submissions/1300714941/){:target="_blank"}

# 설명
1. 이진 탐색 트리인 root를 모든 리프 노드의 깊이 차이가 1 이하인 이진 탐색 트리로 반환하는 문제이다.

2. list는 이진 탐색 트리인 root의 모든 노드를 Inorder 순으로 저장할 변수로, root의 노드들의 값 오름차순으로 list에 노드들을 저장한다.

3. 4번에서 정의한 createBalanceBST(List<TreeNode> list, int start, int end) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

4. 균형잡힌 BST로 만들기 위한 createBalanceBST(List<TreeNode> list, int start, int end) 메서드를 정의한다.
- start가 end 초과인 경우 균형잡힌 범위를 벗어 났으므로, null을 반환한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - mid에 $\frac{start + end}{2}$인 [start, end] 사이의 중앙값을 넣어준다.
  - root에 list의 mid번째 값인 중앙에 위치할 노드를 선택하고, left와 right TreeNode에 순차적으로 [start, $mid - 1$], [$mid + 1$, end]를 이용하여 재귀 호출한 TreeNode를 넣어준다.
  - 수행이 완료되면 [start, end] 범위 내 균형잡힌 BST로 만들어진 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BalanceABinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.