---
title: "Leetcode Java Insertion Sort List"
excerpt: "Leetcode Insertion Sort List Java 풀이"
last_modified_at: 2021-09-05T15:00:00
header:
  image: /assets/images/leetcode/insertion-sort-list.png
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
[Link](https://leetcode.com/problems/insertion-sort-list/){:target="_blank"}

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

  public ListNode insertionSortList(ListNode head) {
    ListNode result = new ListNode();
    ListNode curr = head;
    ListNode next = null;
    ListNode temp = null;
    while (curr != null) {
      next = curr.next;
      temp = result;
      while (temp.next != null && temp.next.val < curr.val) {
        temp = temp.next;
      }
      curr.next = temp.next;
      temp.next = curr;
      curr = next;
    }
    return result.next;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/549720352/){:target="_blank"}

# 설명
1. 주어진 ListNode head를 이용하여 오름차순으로 정열하는 문제이다.

2. 문제 풀이에 필요한 변수들은 정의한다.
- curr은 현재 노드를 저장할 ListNode로, head를 넣어 초기화 시켜준다.
- next는 다음 노드를 저장할 ListNode로, null로 초기화 한다.
- result는 결과를 저장할 ListNode로, 새 ListNode를 넣어준다.
- temp는 임시 변수로 사용할 ListNode로, null로 초기화 한다.

3. 반복문을 통해 curr이 null이 아닐 때 까지 반복한다.
- next에 curr.next를, temp에 result를 넣어준다.
- temp.nexst가 null이 아니고, temp.next.val이 curr.val보다 작을 때 까지 반복하여 temp에 temp.next를 넣어준다.
- curr.next에 temp.next를, temp.next에 curr을, curr에 next를 넣어 순서를 바꾸어준다.

4. 반복이 완료되면 정렬된 ListNode인 result.next를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InsertionSortList.java){:target="_blank"}에서 확인 가능합니다.