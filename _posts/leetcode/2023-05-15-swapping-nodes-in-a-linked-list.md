---
title: "Leetcode Java Swapping Nodes in a Linked List"
excerpt: "Leetcode Swapping Nodes in a Linked List Java"
last_modified_at: 2023-05-15T19:30:00
header:
  image: /assets/images/leetcode/swapping-nodes-in-a-linked-list.png
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
[Link](https://leetcode.com/problems/swapping-nodes-in-a-linked-list){:target="_blank"}

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

  public ListNode swapNodes(ListNode head, int k) {
    ListNode first = null;
    ListNode last = null;
    for (ListNode listNode = head; listNode != null; listNode = listNode.next) {
      if (last != null) {
        last = last.next;
      }
      if (--k == 0) {
        first = listNode;
        last = head;
      }
    }
    int temp = first.val;
    first.val = last.val;
    last.val = temp;
    return head;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/submissions/950712408/){:target="_blank"}

# 설명
1. head의 앞과 뒤에서 k번째 ListNode의 값을 바꾸는 문제이다.

2. first와 last는 앞과 뒤에서 k번째 ListNode를 담을 변수로, 들 다 null로 초기화한다.

3. head부터 null까지 listNode를 다음 ListNode로 이동하면서 아래를 반복한다.
- last가 null이 아니면 last를 다음 ListNode로 이동시킨다.
- k를 감소시키고 k가 0인 경우, first에 listNode를 last에 head를 넣어준다.

4. 반복이 완료되면 temp와 last의 값을 바꾸고 head를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SwappingNodesInALinkedList.java){:target="_blank"}에서 확인 가능합니다.