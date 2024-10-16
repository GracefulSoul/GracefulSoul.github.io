---
title: "Leetcode Java Swap Nodes in Pairs"
excerpt: "Leetcode Swap Nodes in Pairs Java 풀이"
last_modified_at: 2021-05-05T10:10:00
header:
  image: /assets/images/leetcode/swap-nodes-in-pairs.png
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
[Link](https://leetcode.com/problems/swap-nodes-in-pairs/){:target="_blank"}

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

  public ListNode swapPairs(ListNode head) {
    if (head == null || head.next == null) {
      return head;
    }
    List<Integer> list = new ArrayList<>();
    while (head != null) {
      if (head.next == null) {
        list.add(head.val);
        head = head.next;
      } else {
        ListNode temp = head.next;
        list.add(temp.val);
        list.add(head.val);
        head = head.next.next;
      }
    }
    ListNode ln = null;
    for (int idx = list.size(); idx > 0; idx--) {
      ln = new ListNode(list.get(idx - 1), ln);
    }
    return ln;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/488972679/){:target="_blank"}

# 설명
1. 주어진 ListNode head가 null이거나 head.next가 null인 경우, 위치를 변경할 ListNode가 없으므로 주어진 문제의 결과로 head를 반환한다.

2. 반복을 통해 주어진 ListNode haed가 null이 될 때까지 val 값을 List에 모두 넣는다.
- head.next가 null인 경우, 순서를 바꾸지 못하므로 head.val 값만 List에 넣는다.
- head.next가 존재하는 경우, 순서를 바꿔주어야 하므로 head.next.val와 head.val값을 순서를 바꾸어 List에 넣는다.

3. 반복이 완료되면 순서를 바꾸어준 List 기반으로 ListNode를 생성하여, 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SwapNodesinPairs.java){:target="_blank"}에서 확인 가능합니다.