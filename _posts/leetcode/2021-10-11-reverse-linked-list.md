---
title: "Leetcode Java Reverse Linked List"
excerpt: "Leetcode - 'Reverse Linked List' 문제 Java 풀이"
last_modified_at: 2021-10-11T12:00:00
header:
  image: /assets/images/leetcode/reverse-linked-list.png
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
[Link](https://leetcode.com/problems/reverse-linked-list/){:target="_blank"}

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

  public ListNode reverseList(ListNode head) {
    ListNode listNode = null;
    while (head != null) {
      ListNode temp = head.next;
      head.next = listNode;
      listNode = head;
      head = temp;
    }
    return listNode;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/569213974/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head를 역순으로 바꾸는 문제이다.

2. 역순으로 바꾼 ListNode를 저장하기 위한 listNode를 정의한다.

3. head가 null이 아닐 때 까지 반복하여 listNode에 역순으로 넣어준다.
- temp에 head의 next ListNode를 넣어주고, head.next에 listNode를 넣어준다.
- listNode에 다시 head를 넣어주고, head에 temp를 넣어줌으로써 순서를 반전시킨다.

4. 반복이 완료되면 역순으로 저장한 listNode를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseLinkedList.java){:target="_blank"}에서 확인 가능합니다.