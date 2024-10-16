---
title: "Leetcode Java Construct Binary Tree from Inorder and Postorder Traversal"
excerpt: "Leetcode Construct Binary Tree from Inorder and Postorder Traversal Java 풀이"
last_modified_at: 2021-07-27T13:00:00
header:
  image: /assets/images/leetcode/construct-binary-tree-from-inorder-and-postorder-traversal.png
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
[Link](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/){:target="_blank"}

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

  public TreeNode buildTree(int[] inorder, int[] postorder) {
    Map<Integer, Integer> inorderMap = new HashMap<>();
    for (int idx = 0; idx < inorder.length; idx++) {
      inorderMap.put(inorder[idx], idx);
    }
    return this.recursive(postorder, inorderMap, 0, inorder.length - 1, 0, postorder.length - 1);
  }

  private TreeNode recursive(int[] postorder, Map<Integer, Integer> inorderMap, int inStart, int inEnd, int postStart, int postEnd) {
    if (postStart > postEnd || inStart > inEnd) {
      return null;
    }
    TreeNode treeNode = new TreeNode(postorder[postEnd]);
    int inOrderIndex = inorderMap.get(treeNode.val);
    int numsLeft = inOrderIndex - inStart;
    treeNode.left = this.recursive(postorder, inorderMap, inStart, inOrderIndex - 1, postStart, postStart + numsLeft - 1);
    treeNode.right = this.recursive(postorder, inorderMap, inOrderIndex + 1, inEnd, postStart + numsLeft, postEnd - 1);
    return treeNode;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/528894574/){:target="_blank"}

# 설명
1. 주어진 정수 배열 inorder는 TreeNode의 val 값을 Left -> Root -> Right 순서로 정렬한 배열이며, postorder는 TreeNode의 val 값을 Left -> Right -> Root 순서로 정렬한 배열로, 두 배열을 참고하여 TreeNode를 만들어 반환하는 문제이다.

2. 주어진 inorder의 순서를 기억하기 위해 inorderMap을 정의하여 inorder 배열의 해당 값 index를 저장한다.

3. 재귀 호출을 이용하여 TreeNode를 만들어 주어진 문제의 결과로 반환한다.
- postStart가 postEnd보다 크거나 inStart가 inEnd보다 큰 경우 다음 노드의 val 값을 설정하지 못한다는 의미이므로, return 시킨다.
- 문제 풀이에 필요한 기본 변수를 정의한다.
  - 변수 treeNode는 결과로 반환 할 TreeNode를 구성하기 위해 정의하며, postorder[postEnd] 값으로 TreeNode를 생성하여 초기화 한다.
  - 변수 inOrderIndex를 inorder 배열 내 treeNode val 값의 위치를 사용하기 위하여 정의한다.
  - 변수 numsLeft는 inOrderIndex의 위치 값에서 inorder와 postorder 사이의 남은 값이 존재하는지를 의미하며, inOrderIndex에서 inStart를 뺀 값으로 정의한다.
- treeNode의 left의 TreeNode는 inEnd에 $inOrderIndex - 1$을, postEnd에 $postStart + numsLeft - 1$을 넣어 재귀호출을 수행한 결과로 넣어준다.
- treeNode의 right의 TreeNode는 inStart에 $inOrderIndex + 1$을, postStart에 $postStart + numsLeft$를, postEnd에 $postEnd - 1$을 넣어 재귀호출을 수행한 결과로 넣어준다.
- 위의 순서대로 만들어진 TreeNode는 반환 시키고, 최초 호출의 경우 만들어진 TreeNode를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConstructBinaryTreeFromInorderAndPostorderTraversal.java){:target="_blank"}에서 확인 가능합니다.