---
title: "Leetcode Java Remove Duplicates from Sorted List"
excerpt: "Leetcode - 'Remove Duplicates from Sorted List' 문제 Java 풀이"
last_modified_at: 2021-07-03T10:00:00
header:
  image: /assets/images/leetcode/remove-duplicates-from-sorted-list.png
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
[Link](https://leetcode.com/problems/remove-duplicates-from-sorted-list/){:target="_blank"}

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

  public ListNode deleteDuplicates(ListNode head) {
    return this.recursive(head);
  }

  private ListNode recursive(ListNode head) {
    if (head == null) {
      return null;
    } else {
      if ((head.next != null && head.val == head.next.val)) {
        return this.recursive(head.next);
      } else {
        head.next = this.recursive(head.next);
        return head;
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/516540403/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head의 val 값이 중복되지 않은 고유 값로 이루어진 ListNode를 반환하는 문제이다.

2. 재귀 호출을 통해서 주어진 ListNode인 head의 중복된 값을 제거하고 역순으로 ListNode를 만들어 주어진 문제의 결과로 반환한다.
- head가 null인 경우, 주어진 ListNode인 head의 마지막 값이므로 그대로 반환한다.
- head가 null이 아닌 경우, head.next가 존재하고, head.val 값과 head.next의 val 값이 동일하면 현재 값과 다음 값이 동일한 경우이므로 무시하고 재귀 호출을 수행한 값을 반환한다.
- 위의 경우가 아니면 중복된 값이 존재하지 않으므로 head.next에 해당 재귀 호출의 값을 넣고 head를 반환한다.
- 재귀 호출을 통해 역순으로 중복이 제거되어 만들어진 ListNode를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveDuplicatesFromSortedList.java){:target="_blank"}에서 확인 가능합니다.