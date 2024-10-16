---
title: "Leetcode Java Convert Sorted List to Binary Search Tree"
excerpt: "Leetcode Convert Sorted List to Binary Search Tree Java 풀이"
last_modified_at: 2021-07-30T17:00:00
header:
  image: /assets/images/leetcode/convert-sorted-list-to-binary-search-tree.png
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
[Link](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/){:target="_blank"}

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

  public TreeNode sortedListToBST(ListNode head) {
    return this.recursive(head, null);
  }

  private TreeNode recursive(ListNode head, ListNode tail) {
    if (head == null || head == tail) {
      return null;
    }
    ListNode fast = head;
    ListNode slow = head;
    while (fast != tail && fast.next != tail) {
      fast = fast.next.next;
      slow = slow.next;
    }
    TreeNode treeNode = new TreeNode(slow.val);
    treeNode.left = this.recursive(head, slow);
    treeNode.right = this.recursive(slow.next, tail);
    return treeNode;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/530474745/){:target="_blank"}

# 설명
1. 주어진 ListNode를 이용하여 TreeNode를 구현하는 문제이다.

2. 재귀 호출을 이용하여 TreeNode를 만들어 주어진 문제의 결과로 반환한다.
- head가 null이면 풀이에 대한 대상이 null이고, head가 tail과 같으면 좌측 노드 생성이 root 노드 순서에 걸린 경우이므로, null을 반환한다.
- head의 가운데 노드를 root로 하여 TreeNode를 생성하기 위해 fast와 slow에 head를 넣어준다.
- fast와 fast의 next가 tail이 아닐 때 까지 fast는 두 노드를 이동하고, slow는 한 노드를 이동하여 slow를 head의 가운데 노드에 위치하도록 해준다.
- 가운데 위치한 slow를 이용하여 TreeNode를 생성한다.
  - 새 TreeNode인 treeNode를 정의하여 slow의 val 값으로 초기화해준다.
  - treeNode의 left TreeNode에 head와 slow의 재귀 호출을 수행한 결과를 넣어준다.
  - treeNode의 right TreeNode에 slow.next와 tail의 재귀 호출을 수행한 결과를 넣어준다.
- 완성된 treeNode를 반환하고, 초기 재귀 호출의 경우 treeNode를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConvertSortedListToBinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.