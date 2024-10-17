---
title: "Leetcode Java Reverse Linked List II"
excerpt: "Leetcode - 'Reverse Linked List II' 문제 Java 풀이"
last_modified_at: 2021-07-12T18:00:00
header:
  image: /assets/images/leetcode/reverse-linked-list-ii.png
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
[Link](https://leetcode.com/problems/reverse-linked-list-ii/){:target="_blank"}

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

  public ListNode reverseBetween(ListNode head, int left, int right) {
    ListNode temp = new ListNode(0, head);
    ListNode pre = temp;
    ListNode cur = head;
    int idx = 1;
    while (cur.next != null && idx != left) {
      cur = cur.next;
      pre = pre.next;
      idx++;
    }
    while (cur.next != null && idx != right) {
      ListNode preNext = pre.next;
      ListNode curNext = cur.next;
      pre.next = cur.next;
      cur.next = curNext.next;
      curNext.next = preNext;
      idx++;
    }
    return temp.next;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/521220264/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head의 left번째 ListNode부터 right번째 ListNode를 역순으로 반전시키는 문제이다.

2. 문제 해결을 위한 기본 변수를 정의한다.
- 주어진 ListNode인 head를 역순으로 반전시키기 위해 새로운 ListNode의 next값에 head를 넣은 temp를 정의한다.
- head를 반전시키기 위한 임시변수인 pre와 cur을 temp와 head를 각각 넣어 정의한다.
- 반전시키는 구간을 체크하기 위한 index인 idx를 정의한다.

3. 반전시키기 위한 시작 위치인 left 전까지 반복문을 통해 cur과 pre를 다음 값으로 넘겨준다.

4. 반전이 끝나기 위한 종료 위치인 right까지 반복문을 통해 위치를 반전시켜준다.
- pre의 next 값을 임시 저장할 preNext와 cur의 next 값을 임시 저장할 curNext를 정의한다.
- pre의 next에 cur의 next를, cur의 next에 curNext의 next 값을, curNext의 next에 preNext 값을 넣어 위치를 left번째 위치부터 idx번째 위치까지 값을 반전시킨다.
- idx를 증가시키고 반복을 계속한다.

5. 반복이 완료되면 temp의 next를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseLinkedListII.java){:target="_blank"}에서 확인 가능합니다.