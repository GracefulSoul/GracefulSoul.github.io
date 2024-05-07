---
title: "Leetcode Java Double a Number Represented as a Linked List"
excerpt: "Leetcode Double a Number Represented as a Linked List Java"
last_modified_at: 2024-05-07T18:20:00
header:
  image: /assets/images/leetcode/double-a-number-represented-as-a-linked-list.png
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
[Link](https://leetcode.com/problems/double-a-number-represented-as-a-linked-list/){:target="_blank"}

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

  public ListNode doubleIt(ListNode head) {
    if (head.val > 4) {
      head = new ListNode(0, head);
    }
    for (ListNode temp = head; temp != null; temp = temp.next) {
      temp.val = (temp.val * 2) % 10;
      if (temp.next != null && temp.next.val > 4) {
        temp.val++;
      }
    }
    return head;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/double-a-number-represented-as-a-linked-list/submissions/1251623729/){:target="_blank"}

# 설명
1. head의 값들은 이은 정수 값을 두 배로 증가시킨 값을 지닌 ListNode로 반환하는 문제이다.

2. head의 val 값이 4보다 커서 2배를 곱한 값이 자릿수가 증가하는 경우, head에 값은 0 next ListNode는 head를 넣어 초기화한 새 ListNode를 넣어준다.

3. temp에 head를 넣고 temp가 null이 아닐 때 까지 temp에 temp의 다음 ListNode를 넣어가면서 아래를 반복한다.
- temp의 val 값에 해당 값의 2배한 결과의 1의 자리수를 넣어준다.
- temp의 다음 ListNode가 null이 아니면서 temp의 다음 ListNode의 값이 4보다 큰 경우, temp의 val값을 증가시켜준다.

4. 위의 반복을 통해 2배의 값으로 이루어진 head를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DoubleANumberRepresentedAsALinkedList.java){:target="_blank"}에서 확인 가능합니다.