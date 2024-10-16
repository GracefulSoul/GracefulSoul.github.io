---
title: "Leetcode Java Remove Nodes From Linked List"
excerpt: "Leetcode Remove Nodes From Linked List Java"
last_modified_at: 2024-05-06T10:40:00
header:
  image: /assets/images/leetcode/remove-nodes-from-linked-list.png
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
[Link](https://leetcode.com/problems/remove-nodes-from-linked-list/){:target="_blank"}

# 코드
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {

  public ListNode removeNodes(ListNode head) {
    if (head != null) {
      head.next = this.removeNodes(head.next);
      if (head.next != null && head.val < head.next.val) {
        return head.next;
      }
    }
    return head;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/remove-nodes-from-linked-list/submissions/1250452814/){:target="_blank"}

# 설명
1. 각 노드에서 해당 노드의 값보다 작은 좌측 노드를 제거하는 문제이다.

2. head가 null이 아닌 경우, 아래를 수행한다.
- head의 next 노드에 head의 next ListNode를 넣어 재귀 호출한 결과를 넣어준다.
- 아래 경우 모두 만족하는 경우, head의 next ListNode를 반환한다.
  - head의 next 노드가 null이 아닌 마지막 노드가 아닌 값이 비교가 가능한 경우.
  - head의 val 값이 head의 next ListNode val 값보다 작아 제거되는 경우.

3. 위 경우들을 만족하지 않는 경우, head를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveNodesFromLinkedList.java){:target="_blank"}에서 확인 가능합니다.