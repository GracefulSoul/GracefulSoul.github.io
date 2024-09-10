---
title: "Leetcode Java Insert Greatest Common Divisors in Linked List"
excerpt: "Leetcode Insert Greatest Common Divisors in Linked List Java"
last_modified_at: 2024-09-10T17:50:00
header:
  image: /assets/images/leetcode/insert-greatest-common-divisors-in-linked-list.png
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
[Link](https://leetcode.com/problems/insert-greatest-common-divisors-in-linked-list/){:target="_blank"}

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

  public ListNode insertGreatestCommonDivisors(ListNode head) {
    if (head.next != null) {
      ListNode node = head;
      while (node.next != null) {
        ListNode temp = new ListNode(this.getGcd(node.val, node.next.val), node.next);
        node.next = temp;
        node = temp.next;
      }
    }
    return head;
  }

  private int getGcd(int m, int n) {
    if (n == 0) {
      return m;
    } else {
      return this.getGcd(n, m % n);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/spiral-matrix-iv/submissions/1384195866/){:target="_blank"}

# 설명
1. head의 각 노드 사이에 최대 공약수를 넣어주는 문제이다.

2. head의 next 노드가 null이 아닌, 두 노드 이상인 경우만 아래를 수행한다.
- node의 next 노드가 null이 아닐 때 까지 node의 val 값과 node.next 노드의 val 값을 이용한 최대 공약수를 두 노드 사이에 이어준다.

3. 반복이 완료되면 각 노드 사이에 최대 공약수가 들어간 head를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InsertGreatestCommonDivisorsInLinkedList.java){:target="_blank"}에서 확인 가능합니다.