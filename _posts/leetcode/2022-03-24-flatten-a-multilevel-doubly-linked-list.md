---
title: "Leetcode Java Flatten a Multilevel Doubly Linked List"
excerpt: "Leetcode Flatten a Multilevel Doubly Linked List Java 풀이"
last_modified_at: 2022-03-24T12:00:00
header:
  image: /assets/images/leetcode/flatten-a-multilevel-doubly-linked-list.png
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
[Link](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/){:target="_blank"}

# 코드
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;
};
*/

class Solution {

  public Node flatten(Node head) {
    if (head == null) {
      return null;
    } else if (head.child == null) {
      Node node = this.flatten(head.next);
      head.next = node;
      if (node != null) {
        node.prev = head;
      }
    } else {
      Node node = head.next;
      Node child = this.flatten(head.child);
      head.next = child;
      child.prev = head;
      Node temp = child;
      while (temp.next != null) {
        temp = temp.next;
      }
      Node next = this.flatten(node);
      temp.next = next;
      if (next != null) {
        next.prev = temp;
      }
      head.child = null;
    }
    return head;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/666035942/){:target="_blank"}

# 설명
1. 주어진 이전, 다음, 자식 노드 정보를 가지고 있는 head Node를 직렬화 시키는 문제이다.
- 직렬화 시킬 때, 자식 노드 -> 다음 노드 순의 순서로 진행한다.

2. head가 null인 경우 직렬화가 불가능하기 때문에, null을 반환한다.

3. head의 child 노드가 null인 경우, 아래를 수행하여 다음 노드로 직렬화를 수행한다.
- node에 head의 next 노드를 이용하여 재귀 호출한 결과를 넣어준다.
- head의 next 노드에 node를 넣어준다.
- node가 null이 아닌 경우, node의 이전 값에 head를 넣어 이어준다.

4. 그 외의 head의 child 노드가 존재하는 경우, 아래를 수행하여 순차적으로 직렬화를 수행한다.
- node에 head의 next 노드를 임시로 넣어준다.
- child에 head의 child 노드를 이용하여 재귀 호출한 결과를 넣어준다.
  - child -> next 순으로 직렬화 하기 때문에, child를 먼저 직렬화 한다.
- head의 next에 child 노드를, child의 prev 노드에 head를 넣어 각 노드를 이어준다.
- temp에 child를 넣어주고, temp의 next 노드가 null이 아닐 때 까지 반복하여 temp에 temp의 next 노드를 넣어 마지막 노드로 이동시킨다.
- next에 node의 재귀 호출을 수행한 결과를 넣어준다.
- temp의 next 노드에 next를 넣어준다.
- next가 null이 아닌 경우, next의 prev 노드에 temp를 넣어 위의 child를 직렬화 한 노드에 이어준다.
- head의 child 노드에 null을 넣어 자식 노드를 제거한다.

5. 수행이 완료되면 부분 직렬화를 수행한 head를 반환하고, 최종 직렬화가 완료되면 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlattenAMultilevelDoublyLinkedList.java){:target="_blank"}에서 확인 가능합니다.