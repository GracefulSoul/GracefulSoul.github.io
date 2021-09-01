---
title: "Leetcode Java Reorder List"
excerpt: "Leetcode Reorder List Java 풀이"
last_modified_at: 2021-09-01T12:00:00
header:
  image: /assets/images/leetcode/reorder-list.png
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
[Link](https://leetcode.com/problems/reorder-list/){:target="_blank"}

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

  public void reorderList(ListNode head) {
    if (head == null || head.next == null) {
      return;
    }
    ListNode node = this.reverseHalfAfterMiddleListNodes(head);
    ListNode temp1 = head;
    ListNode temp2 = node.next;
    while (temp1 != node) {
      node.next = temp2.next;
      temp2.next = temp1.next;
      temp1.next = temp2;
      temp1 = temp2.next;
      temp2 = node.next;
    }
  }

  private ListNode reverseHalfAfterMiddleListNodes(ListNode node) {
    ListNode mid = this.findMiddleListNode(node);
    ListNode cur = mid.next;
    while (cur.next != null) {
      ListNode temp = cur.next;
      cur.next = temp.next;
      temp.next = mid.next;
      mid.next = temp;
    }
    return mid;
  }

  private ListNode findMiddleListNode(ListNode node) {
    ListNode fast = node;
    ListNode slow = node;
    while (fast.next != null && fast.next.next != null) {
      fast = fast.next.next;
      slow = slow.next;
    }
    return slow;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/547526259/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head를 아래의 순서대로 재 정렬하는 문제이다.
- node[0] -> node[last] -> node[1] -> node[last] -> ... -> node[$n - 2$] -> node[last]
- node[last]는 각 노드 수행에 있어 마지막에 위치한 노드의 값이다.
- Ex) 1, 2, 3, 4, <b>5</b> -> 1, <b>5</b>, 2, 3, <b>4</b> -> 1, 5, 2, <b>4</b>, 3

2. 주어진 ListNode인 head의 중간 위치를 탐색한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - fast는 slow보다 끝을 먼저 탐색하기 위해 이동하는 임시 ListNode로, head를 주입해준다.
  - slow는 fast ListNode 기준으로 중간 ListNode에 위치하는 ListNode로, head를 주입해준다.
- fast.next와 fast.next.next가 null이 아닐 때 까지 fast는 2칸, slow는 1칸 이동하여 slow를 head의 중간 ListNode로 이동시켜준다.

3. 2번에서 탐색한 주어진 ListNode인 head의 중간 ListNode를 이용하여 중간 이후의 ListNode들의 순서를 반전시켜준다.
- 문제 풀이에 필요한 변수를 정의한다.
  - mid는 2번에서 탐색한 head의 중간 ListNode의 값을 넣어준다.
  - cur은 반전시키기 위한 mid의 다음 ListNode를 저장하는 ListNode로, mid.next로 값을 넣어준다.
- cur.next가 null이 아닐 때 까지 반복하여 mid와 cur의 next값을 바꾸어, mid의 모든 ListNode의 순서를 반전시켜준다.

4. 3번에서 반전시킨 node를 가져와서 1번에서 설명한 순서대로 재 정렬을 수행한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - node는 3번에서 head의 중간 이후 ListNode를 반전시킨 노드를 넣어준다.
  - temp1은 재 정렬을 수행하기 위한 임시 변수로, head를 넣어준다.
  - temp2 또한 재 정렬을 수행하기 위한 임시 변수로, node의 next ListNode를 넣어준다.
- temp1이 node와 같지 않을 때 까지 각 변수들의 값을 바꾸어주며 1번에서 설명한 순서대로 정렬을 수행한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReorderList.java){:target="_blank"}에서 확인 가능합니다.