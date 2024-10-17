---
title: "Leetcode Java Delete Node in a BST"
excerpt: "Leetcode - 'Delete Node in a BST' 문제 Java 풀이"
last_modified_at: 2022-04-09T13:00:00
header:
  image: /assets/images/leetcode/delete-node-in-a-bst.png
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
[Link](https://leetcode.com/problems/delete-node-in-a-bst/){:target="_blank"}

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

  public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) {
      return null;
    } else if (key < root.val) {
      root.left = this.deleteNode(root.left, key);
    } else if (key > root.val) {
      root.right = this.deleteNode(root.right, key);
    } else if (root.left == null) {
      return root.right;
    } else if (root.right == null) {
      return root.left;
    } else {
      root.val = this.findMinValue(root.right);
      root.right = this.deleteNode(root.right, root.val);
    }
    return root;
  }

  private int findMinValue(TreeNode root) {
    while (root.left != null) {
      root = root.left;
    }
    return root.val;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/676682079/){:target="_blank"}

# 설명
1. TreeNode인 root 내 val 값이 key와 동일한 노드를 제거하는 문제이다.

2. root를 각 경우 별 검증을 통해 절차를 수행한다.
- root가 null인 경우 노드가 없으므로, null을 반환한다.
- key가 root의 val 값보다 작은 경우 해당 root 기준으로 key는 좌측 TreeNode에 존재하므로, root의 left TreeNode로 재귀 호출을 수행한다.
- key가 root의 val 값보다 큰 경우 해당 root 기준으로 key는 우측 TreeNode에 존재하므로, root의 right TreeNode로 재귀 호출을 수행한다.
- root의 left TreeNode가 null인 경우, root의 right TreeNode를 반환하여 검증하도록 한다.
- root의 right TreeNode가 null인 경우, root의 left TreeNode를 반환하여 검증하도록 한다.
- 그 외의 경우 root의 val 값이 key이므로, 아래를 수행하여 노드를 삭제하고 다음 노드를 이어준다.
  - root의 val 값에 3번에서 정의한 findMinValue(TreeNode root) 메서드를 수행한 결과를 넣어준다.
  - root의 right TreeNode에 root의 right TreeNode를 재귀 호출을 수행한 결과를 넣어준다.

3. root 기준으로 가장 작은 값을 찾는 findMinValue(TreeNode root) 메서드를 정의한다.
- root의 left TreeNode가 null이 아닐 때 까지 반복하여, root에 root의 left TreeNode를 넣어준다.
- root 기준의 가장 작은 값을 찾은 root의 val 값을 반환한다.

4. 수행이 완료되면 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteNodeInABST.java){:target="_blank"}에서 확인 가능합니다.