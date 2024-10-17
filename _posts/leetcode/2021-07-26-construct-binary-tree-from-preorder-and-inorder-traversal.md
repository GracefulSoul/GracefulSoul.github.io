---
title: "Leetcode Java Construct Binary Tree from Preorder and Inorder Traversal"
excerpt: "Leetcode - 'Construct Binary Tree from Preorder and Inorder Traversal' 문제 Java 풀이"
last_modified_at: 2021-07-26T17:00:00
header:
  image: /assets/images/leetcode/construct-binary-tree-from-preorder-and-inorder-traversal.png
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
[Link](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/){:target="_blank"}

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

  public TreeNode buildTree(int[] preorder, int[] inorder) {
    Map<Integer, Integer> inorderMap = new HashMap<>();
    for (int idx = 0; idx < inorder.length; idx++) {
      inorderMap.put(inorder[idx], idx);
    }
    return this.recursive(preorder, inorderMap, 0, preorder.length - 1, 0);
  }

  private TreeNode recursive(int[] preorder, Map<Integer, Integer> inorderMap, int preStart, int preEnd, int inStart) {
    if (preStart > preEnd) {
      return null;
    }
    TreeNode treeNode = new TreeNode(preorder[preStart]);
    int inOrderIndex = inorderMap.get(treeNode.val);
    int numsLeft = inOrderIndex - inStart;
    treeNode.left = this.recursive(preorder, inorderMap, preStart + 1, preStart + numsLeft, inStart);
    treeNode.right = this.recursive(preorder, inorderMap, preStart + numsLeft + 1, preEnd, inOrderIndex + 1);
    return treeNode;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/528473265/){:target="_blank"}

# 설명
1. 주어진 정수 배열 preorder는 TreeNode의 val 값을 Root -> Left -> Right 순서로 정렬한 배열이며, inorder는 TreeNode의 val 값을 Left -> Root -> Right 순서로 정렬한 배열로, 두 배열을 참고하여 TreeNode를 만들어 반환하는 문제이다.

2. 주어진 inorder의 순서를 기억하기 위해 inorderMap을 정의하여 inorder 배열의 해당 값 index를 저장한다.

3. 재귀 호출을 이용하여 TreeNode를 만들어 주어진 문제의 결과로 반환한다.
- preStart가 preEnd보다 큰 경우 다음 노드의 val 값을 설정하지 못한다는 의미이므로, return 시킨다.
- 문제 풀이에 필요한 기본 변수를 정의한다.
  - 변수 treeNode는 결과로 반환 할 TreeNode를 구성하기 위해 정의하며, preorder[preStart] 값으로 TreeNode를 생성하여 초기화 한다.
  - 변수 inOrderIndex를 inorder 배열 내 treeNode val 값의 위치를 사용하기 위하여 정의한다.
  - 변수 numsLeft는 inOrderIndex의 위치 값에서 preorder와 inorder 사이의 남은 값이 존재하는지를 의미하며, inOrderIndex에서 inStart를 뺀 값으로 정의한다.
- treeNode의 left의 TreeNode는 preStart에 1을 증가시키고, preEnd에 $preStart + numsLeft$를 넣어 재귀호출을 수행한 결과로 넣어준다.
- treeNode의 right의 TreeNode는 preStart에 $preStart + numsLeft + 1$을, inStart에 $inOrderIndex + 1$을 넣어 재귀호출을 수행한 결과로 넣어준다.
- 위의 순서대로 만들어진 TreeNode는 반환 시키고, 최초 호출의 경우 만들어진 TreeNode를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConstructBinaryTreeFromPreorderAndInorderTraversal.java){:target="_blank"}에서 확인 가능합니다.