---
title: "Leetcode Java Linked List Cycle"
excerpt: "Leetcode Linked List Cycle Java 풀이"
last_modified_at: 2021-08-30T13:00:00
header:
  image: /assets/images/leetcode/linked-list-cycle.png
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
[Link](https://leetcode.com/problems/linked-list-cycle/){:target="_blank"}

# 코드
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
class Solution {

  public boolean hasCycle(ListNode head) {
    if (head == null) {
      return false;
    }
    ListNode fast = head;
    ListNode slow = head;
    while (fast.next != null && fast.next.next != null) {
      fast = fast.next.next;
      slow = slow.next;
      if (fast == slow) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/546453516/){:target="_blank"}

# 설명
1. 주어진 ListNode head가 순회하는 포인트가 존재하는지를 검증하는 문제이다.

2. head가 null인 경우 순회가 불가능하므로, false를 주어진 문제의 결과로 반환한다.

3. 검증을 위해 fast와 slow를 head를 주입하여 정의한다.

4. fast.next와 fast.next.next가 null이 아닐 때 까지 반복하여 검증을 수행한다.
- fast에 fast.next.next 값을 주입하여 다다음 ListNode로 이동한다.
- slow에 slow.next 값을 주입하여 다음 ListNode로 이동한다.
- slow와 fast가 동일하면 순회가 되는 포인트가 있는 경우이므로, true를 주어진 문제의 결과로 반환한다.

5. 반복이 종료되면 null이 되는 순간이 존재한다는 의미이므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LinkedListCycle.java){:target="_blank"}에서 확인 가능합니다.