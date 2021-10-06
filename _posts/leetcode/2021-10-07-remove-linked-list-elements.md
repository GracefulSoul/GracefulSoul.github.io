---
title: "Leetcode Java Remove Linked List Elements"
excerpt: "Leetcode Remove Linked List Elements Java 풀이"
last_modified_at: 2021-10-07T08:30:00
header:
  image: /assets/images/leetcode/remove-linked-list-elements.png
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
[Link](https://leetcode.com/problems/remove-linked-list-elements/){:target="_blank"}

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
public class Solution {

  public ListNode removeElements(ListNode head, int val) {
    if (head == null) {
      return null;
    }
    ListNode next = this.removeElements(head.next, val);
    if (head.val == val) {
      return next;
    } else {
      head.next = next;
      return head;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/567033188/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head에서 val값을 가진 ListNode를 제거하고 앞과 뒤의 ListNode를 이어주는 문제이다.

2. 주어진 ListNode인 head가 null인 경우, null을 반환한다.

3. head.next를 이용하여 재귀 호출을 수행한 결과를 next에 넣어둔다.
- head.val의 값과 val 값이 동일한 경우, 다음 노드의 결과인 next를 반환한다.
- head.val의 값과 val 값이 동일하지 않은 경우, head.next에 그대로 next를 넣고 head를 반환한다.

4. 재귀 호출이 완료되면 val값이 포함된 ListNode를 제거한 head가 완성된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveLinkedListElements.java){:target="_blank"}에서 확인 가능합니다.