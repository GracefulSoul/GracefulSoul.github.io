---
title: "Leetcode Java Middle of the Linked List"
excerpt: "Leetcode Middle of the Linked List Java"
last_modified_at: 2023-03-18T07:20:00
header:
  image: /assets/images/leetcode/middle-of-the-linked-list.png
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
[Link](https://leetcode.com/problems/middle-of-the-linked-list){:target="_blank"}

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

  public ListNode middleNode(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;
    while (fast != null && fast.next != null) {
      slow = slow.next;
      fast = fast.next.next;
    }
    return slow;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/middle-of-the-linked-list/submissions/917111684/){:target="_blank"}

# 설명
1. head의 중앙에 있는 ListNode를 반환하는 문제이다.
- 중앙에 두 ListNode가 존재하면 두 번째 ListNode를 반환한다.

2. slow는 한 단계 씩 이동하기 위한 ListNode이고, fast는 두 단계 씩 이동하기 위한 ListNode로 둘 다 head로 초기화한다.

3. fast와 fast의 다음 ListNode가 null이 아닐 때 까지 slow에 slow의 다음 ListNode를, fast에 fast의 다다음 ListNode를 넣어준다.

4. 반복이 완료되면 head의 중앙에 위치한 slow를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MiddleOfTheLinkedList.java){:target="_blank"}에서 확인 가능합니다.