---
title: "Leetcode Java Linked List Cycle II"
excerpt: "Leetcode Linked List Cycle II Java 풀이"
last_modified_at: 2021-08-31T09:00:00
header:
  image: /assets/images/leetcode/linked-list-cycle-ii.png
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
[Link](https://leetcode.com/problems/linked-list-cycle-ii/){:target="_blank"}

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
      return null;
    }
    ListNode fast = head;
    ListNode slow = head;
    while (fast != null && fast.next != null) {
      fast = fast.next.next;
      slow = slow.next;
      if (fast == slow) {
        ListNode search = head;
        while (slow != search) {
          slow = slow.next;
          search = search.next;
        }
        return search;
      }
    }
    return null;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/546937975/){:target="_blank"}

# 설명
1. 주어진 ListNode head가 순회의 시작점인 ListNode를 찾는 문제이다.

2. head가 null인 경우 순회가 불가능하므로, null을 주어진 문제의 결과로 반환한다.

3. 검증을 위해 fast와 slow를 head를 주입하여 정의한다.

4. fast와 fast.next가 null이 아닐 때 까지 반복하여 검증을 수행한다.
- fast에 fast.next.next 값을 주입하여 다다음 ListNode로 이동한다.
- slow에 slow.next 값을 주입하여 다음 ListNode로 이동한다.
- fast와 slow가 동일하면 순회가 되는 포인트가 있는 경우이므로, 순회의 시작점을 탐색한다.
  - search 변수를 임시 정의하여 주어진 ListNode인 head를 주입한다.
  - slow와 search가 동일한 결과가 나올 때 까지 slow와 search를 각각 다음 ListNode로 이동시킨다.
  - 반복이 완료되면 순회의 시작점인 search를 주어진 문제의 결과로 반환한다.

5. 모든 반복이 완료되고 결과가 나오지 않는 경우 순회가 되지 않는다는 의미이므로, null을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LinkedListCycleII.java){:target="_blank"}에서 확인 가능합니다.