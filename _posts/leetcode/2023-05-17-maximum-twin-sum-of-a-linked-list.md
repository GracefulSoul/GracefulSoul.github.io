---
title: "Leetcode Java Maximum Twin Sum of a Linked List"
excerpt: "Leetcode Maximum Twin Sum of a Linked List Java"
last_modified_at: 2023-05-17T20:30:00
header:
  image: /assets/images/leetcode/maximum-twin-sum-of-a-linked-list.png
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
[Link](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list){:target="_blank"}

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

  public int pairSum(ListNode head) {
    ListNode fast = head;
    ListNode slow = head;
    ListNode curr = head;
    ListNode prev = null;
    while (fast != null) {
      fast = fast.next.next;
      curr = slow;
      slow = slow.next;
      curr.next = prev;
      prev = curr;
    }
    int result = 0;
    while (slow != null) {
      result = Math.max(result, prev.val + slow.val);
      slow = slow.next;
      prev = prev.next;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/submissions/952029289/){:target="_blank"}

# 설명
1. 짝수 길이의 head를 이용하여 최대 쌍둥이 합을 구하는 문제이다.
- 길이가 n일 경우, 0 <= i <= $\frac{n}{2} - 1$이면 i번째 노드는 $n - 1 - i$번째 노드의 쌍둥이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- fast와 slow는 ListNode인 head의 중앙 지점을 slow에 위치하게 하기 위한 변수로, 둘 다 head로 초기화한다.
- curr과 prev는 ListNode인 head의 중앙 이전 값을 prev에 역순으로 저장하기 위한 변수로, curr은 head prev는 null로 초기화한다.

3. fast가 null일 때 까지 slow에 head의 $\frac{n}{2} + 1$ 위치에 위치시키고, prev에 $\frac{n}{2}$ 이전까지 역순으로 저장시킨다.

4. result는 최대 쌍둥이 합을 저장하기 위한 변수로, 0으로 초기화한다.

5. slow가 null이지 않을 때 까지 slow와 prev의 값들인 중앙 위치의 두 쌍둥이 합을 계산하여 result에 최댓값을 넣어준다.

6. 반복이 완료되면 최대 쌍둥이 합이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumTwinSumOfALinkedList.java){:target="_blank"}에서 확인 가능합니다.