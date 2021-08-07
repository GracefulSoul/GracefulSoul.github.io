---
title: "Leetcode Java Populating Next Right Pointers in Each Node II"
excerpt: "Leetcode Populating Next Right Pointers in Each Node II Java 풀이"
last_modified_at: 2021-08-07T12:00:00
header:
  image: /assets/images/leetcode/populating-next-right-pointers-in-each-node-ii.png
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
[Link](https://leetcode.com/populating-next-right-pointers-in-each-node-ii/){:target="_blank"}

# 코드
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/
class Solution {

  public Node connect(Node root) {
    this.recursive(root, null);
    return root;
  }

  private void recursive(Node curr, Node pre) {
    if (curr == null) {
      return;
    }
    if (curr.left != null) {
      curr.left.next = curr.right;
    }
    while (curr.next == null && pre != null && pre.next != null) {
      pre = pre.next;
      curr.next = (pre.left != null) ? pre.left : pre.right;
    }
    this.recursive(curr.right, curr);
    this.recursive(curr.left, curr);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/534076549/){:target="_blank"}

# 설명
1. 지난번 [Populating Next Right Pointers in Each Node](../populating-next-right-pointers-in-each-node) 문제와 유사하게, 주어진 Node인 root를 이용하여 각 node를 이어주는 문제이다.
- 단, 연결하는 중간에 빠진 노드가 존재하므로 해당 노드를 건너 뛰고 연결하여야 한다.

2. 재귀 호출을 이용하여 주어진 Node인 root의 next가 null인 경우, 동일 Level 내에서 다음에 존재하는 Node를 넣어 이어준다.
- curr이 null인 경우 해당 노드가 존재하지 않으므로, 그만 수행한다.
- curr의 left TreeNode가 null이 아닌 경우 curr TreeNode의 left와 right 자식 노드가 모두 존재한다는 의미이므로, curr.left의 next TreeNode에 curr의 right TreeNode를 넣어준다.
- curr의 next TreeNode가 null이고, pre TreeNode가 null이 아니고, pre의 right TreeNode가 null이 아닌 경우 계속 반복문을 통해서 아래를 수행한다.
  - pre TreeNode에 pre의 next TreeNode를 넣어준다.
  - curr의 next TreeNode에 pre의 left가 null이 아니면 pre의 left TreeNode를, 아니면 pre의 right TreeNode를 넣어준다.
- curr의 right TreeNode와 curr을 이용하여 재귀 호출을 수행한다.
- curr의 left TreeNode와 curr을 이용하여 재귀 호출을 수행한다.

3. 재귀 호출이 완료되면 엮어진 Node인 root를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PopulatingNextRightPointersInEachNodeII.java){:target="_blank"}에서 확인 가능합니다.