---
title: "Leetcode Java Merge In Between Linked Lists"
excerpt: "Leetcode Merge In Between Linked Lists Java"
last_modified_at: 2024-03-20T21:45:00
header:
  image: /assets/images/leetcode/merge-in-between-linked-lists.png
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
[Link](https://leetcode.com/problems/merge-in-between-linked-lists/){:target="_blank"}

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

  public ListNode mergeInBetween(ListNode list1, int a, int b, ListNode list2) {
    ListNode head = list1;
    for (int i = 1; i < a; i++) {
      head = head.next;
    }
    ListNode tail = head;
    for (int i = a; i <= b; i++) {
      tail = tail.next;
    }
    head.next = list2;
    while (list2.next != null) {
      list2 = list2.next;
    }
    list2.next = tail.next;
    return list1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/merge-in-between-linked-lists/submissions/1209080606/){:target="_blank"}

# 설명
1. list1 리스트노드에서 a번째 노드에서 b번째 노드까지 제거하고 그 사이에 list2 리스트노드를 이어주는 문제이다.

2. head에 list1을 넣고 1부터 a 미만일 때 까지 i를 증가시키며, haed에 head의 next 노드를 넣어 무시해야 할 위치에 해당하는 노드를 정해준다.

3. tail에 head를 넣고 a부터 b 이하일 때 까지 i를 증가시키며, tail에 tail의 next 노드를 넣어 무시해야 할 위치가 끝나는 노드의 위치에 해당하는 노드를 저장한다.

4. head의 next에 list2를 넣어 이어주고, list2의 마지막 위치의 next 노드에 tail의 next 노드를 넣고 list1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MergeInBetweenLinkedLists.java){:target="_blank"}에서 확인 가능합니다.