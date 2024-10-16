---
title: "Leetcode Java Remove Zero Sum Consecutive Nodes from Linked List"
excerpt: "Leetcode Remove Zero Sum Consecutive Nodes from Linked List Java"
last_modified_at: 2024-03-12T18:40:00
header:
  image: /assets/images/leetcode/remove-zero-sum-consecutive-nodes-from-linked-list.png
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
[Link](https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list){:target="_blank"}

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

  public ListNode removeZeroSumSublists(ListNode head) {
    if (head == null) {
      return head;
    }
    ListNode curr = head;
    int sum = 0;
    while (curr != null) {
      sum += curr.val;
      if (sum == 0) {
        return this.removeZeroSumSublists(curr.next);
      } else {
        curr = curr.next;
      }
    }
    head.next = this.removeZeroSumSublists(head.next);
    return head;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list/submissions/1201384225/){:target="_blank"}

# 설명
1. head 내 연속된 값의 합이 0이 되는 노드를 제거하는 문제이다.

2. head가 null인 경우, head를 그대로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- curr은 현재 ListNode를 저장할 변수로, head로 넣어준다.
- sum은 노드의 합을 저장할 변수로, 0으로 초기화한다.

4. curr이 null이 아닐 때까지 아래를 반복한다.
- sum에 curr의 val 값을 더해준다.
- sum이 0인 경우, 현재까지의 노드들을 무시하기 위해서 curr의 다음 ListNode로 재귀 호출한 결과를 반환한다.
- sum이 0이 아닌 경우, curr에 curr의 다음 ListNode를 넣어 반복을 계속 수행한다.

5. 반복이 완료되면 head의 다음 ListNode에 해당 ListNode로 재귀 호출한 결과를 넣어준 후 완성된 head를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveZeroSumConsecutiveNodesFromLinkedList.java){:target="_blank"}에서 확인 가능합니다.