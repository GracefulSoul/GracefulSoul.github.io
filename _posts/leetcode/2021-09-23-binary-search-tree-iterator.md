---
title: "Leetcode Java Binary Search Tree Iterator"
excerpt: "Leetcode - 'Binary Search Tree Iterator' 문제 Java 풀이"
last_modified_at: 2021-09-23T12:00:00
header:
  image: /assets/images/leetcode/binary-search-tree-iterator.png
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
[Link](https://leetcode.com/problems/binary-search-tree-iterator/){:target="_blank"}

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
class BSTIterator {

  private Stack<TreeNode> stack = new Stack<>();

  public BSTIterator(TreeNode root) {
    this.pushAllTreeNode(root);
  }

  public int next() {
    TreeNode treeNode = stack.pop();
    this.pushAllTreeNode(treeNode.right);
    return treeNode.val;

  }

  public boolean hasNext() {
    return !stack.isEmpty();
  }

  private void pushAllTreeNode(TreeNode treeNode) {
    while (treeNode != null) {
      stack.push(treeNode);
      treeNode = treeNode.left;
    }
  }

}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/559467872/){:target="_blank"}

# 설명
1. 주어진 BSTIterator Class를 완성하는 문제이다.
- 해당 Class는 [이진 검색 트리(BST)](https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%ED%83%90%EC%83%89_%ED%8A%B8%EB%A6%AC)를 순회하는 객체이다.
- 순차적인 TreeNode를 반환하기 위하여 TreeNode를 Stack에 보관하여 사용한다.

2. BSTIterator(TreeNode root) 생성자를 완성한다.
- 생성자는 주어진 TreeNode인 root를 이용하여 객체를 초기화 한다.
- TreeNode를 Root에서 Left 순으로 저장하여 FILO로 stack에 저장한다.

3. hasNext() 메서드를 완성한다.
- TreeNode의 다음 TreeNode이 존재하는지를 검증하는 메서드로, stack이 비어있지 않으면 다음 TreeNode가 존재한다고 판단한다.

4. next() 메서드를 완성한다.
- stack에서 가장 마지막으로 저장된 TreeNode를 가져와서 반환한다.
- 단, 반환하기 전에 해당 TreeNode의 right TreeNode를 stack에 저장시켜야 다음 next() 메서드 호출 시, 해당 TreeNode의 right TreeNode를 반환할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinarySearchTreeIterator.java){:target="_blank"}에서 확인 가능합니다.