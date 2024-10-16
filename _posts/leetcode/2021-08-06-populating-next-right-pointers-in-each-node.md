---
title: "Leetcode Java Populating Next Right Pointers in Each Node"
excerpt: "Leetcode Populating Next Right Pointers in Each Node Java 풀이"
last_modified_at: 2021-08-06T17:00:00
header:
  image: /assets/images/leetcode/populating-next-right-pointers-in-each-node.png
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
[Link](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/){:target="_blank"}

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

  private void recursive(Node curr, Node next) {
    if (curr == null) {
      return;
    }
    curr.next = next;
    this.recursive(curr.left, curr.right);
    this.recursive(curr.right, curr.next == null ? null : curr.next.left);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/534076549/){:target="_blank"}

# 설명
1. 주어진 Node인 root를 이용하여 각 node를 이어주는 문제이다.

2. 재귀 호출을 이용하여 주어진 Node인 root의 next가 null인 경우, 다음 Level의 좌측 첫 Node를 넣어 이어준다.
- curr이 null인 경우 해당 노드가 존재하지 않으므로, 그만 수행한다.
- curr의 next에 next를 넣어 다음 노드로 이동시킨다.
- curr의 left Node와 right Node를 재귀 호출을 수행하여 left Node의 next에 right Node가 연결되도록 엮어준다.
- curr의 next Node가 null이 아닌 경우, curr.next의 left Node가 curr의 right Node의 next에 연결되도록 엮어준다.
- curr의 next Node가 null인 경우, 그대로 next 자리에 null을 넣어 재귀 호출을 수행한다.

3. 재귀 호출이 완료되면 엮어진 Node인 root를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PopulatingNextRightPointersInEachNode.java){:target="_blank"}에서 확인 가능합니다.