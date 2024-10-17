---
title: "Leetcode Java Recover Binary Search Tree"
excerpt: "Leetcode - 'Recover Binary Search Tree' 문제 Java 풀이"
last_modified_at: 2021-07-19T17:00:00
header:
  image: /assets/images/leetcode/recover-binary-search-tree.png
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
[Link](https://leetcode.com/problems/recover-binary-search-tree/){:target="_blank"}

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

  public void recoverTree(TreeNode root) {
    TreeNode previous = null;
    TreeNode first = null;
    TreeNode second = null;
    TreeNode temp = null;
    while (root != null) {
      if (root.left != null) {
        temp = root.left;
        while (temp.right != null && temp.right != root) {
          temp = temp.right;
        }
        if (temp.right != null) {
          if (previous != null && previous.val > root.val) {
            if (first == null) {
              first = previous;
            }
            second = root;
          }
          previous = root;
          temp.right = null;
          root = root.right;
        } else {
          temp.right = root;
          root = root.left;
        }
      } else {
        if (previous != null && previous.val > root.val) {
          if (first == null) {
            first = previous;
          }
          second = root;
        }
        previous = root;
        root = root.right;
      }
    }
    if (first != null && second != null) {
      int t = first.val;
      first.val = second.val;
      second.val = t;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/524830104/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root는 [이진 검색 트리](https://en.wikipedia.org/wiki/Binary_search_tree){:target="_blank"}로, 잘못된 두 값의 위치를 변경하여 정상적으로 만드는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- 이전의 TreeNode를 저장할 변수인 previous를 정의한다.
- 두 잘못된 TreeNode를 저장할 변수인 first, second를 정의한다.
- TreeNode를 임시 저장하여 사용 할 변수인 temp를 정의한다.

3. root가 null이 아닐 경우까지 반복을 수행하여 잘못된 두 값의 위치를 확인하여 변경한다.

4. root의 left가 null이 아닐 경우, 아래의 내용을 수행한다.
- temp에 root의 left TreeNode를 저장한다.
- temp의 right TreeNode가 null이나 root이면 temp의 right TreeNode를 temp에 넣어준다.
- temp의 right TreeNode가 null이 아닌 경우, 아래의 내용을 수행한다.
  - previous가 null이 아니고 previous의 val 값이 root의 val 값보다 큰 경우 잘못된 노드이므로 first가 null이면 first에 previous를 second에 root를 넣어준다.
  - previous에 root를, temp.right에 null을, root에 root의 right TreeNode를 넣어준다.
- temp의 right TreeNode가 null인 경우, temp.right에 root를, root에 root의 left TreeNode를 넣어준다.

5. root의 left가 null인 경우, 아래의 내용을 수행한다.
- previous가 null이 아니고 previous의 val 값이 root의 val 값보다 큰 경우 잘못된 노드이므로 first가 null이면 first에 previous를 second에 root를 넣어준다.
- previous에 root를, root에 root의 right TreeNode를 넣어준다.

6. 반복이 완료되고 first와 second가 null이 아닌 경우, 잘못된 두 위치를 찾은 경우이므로 first의 val 값과 seconde의 val 값을 정상 노드로 바꾸어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RecoverBinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.