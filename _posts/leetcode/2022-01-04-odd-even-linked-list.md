---
title: "Leetcode Java Odd Even Linked List"
excerpt: "Leetcode - 'Odd Even Linked List' 문제 Java 풀이"
last_modified_at: 2022-01-04T20:00:00
header:
  image: /assets/images/leetcode/odd-even-linked-list.png
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
[Link](https://leetcode.com/problems/odd-even-linked-list/){:target="_blank"}

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

  public ListNode oddEvenList(ListNode head) {
    if (head != null) {
      ListNode odd = head;
      ListNode even = head.next;
      ListNode temp = head.next;
      while (even != null && even.next != null) {
        odd.next = even.next;
        even.next = even.next.next;
        odd = odd.next;
        even = even.next;
      }
      odd.next = temp;
    }
    return head;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/612825695/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head를 이용하여 짝수번째 값들을 head의 뒤로 이동시키는 문제이다.
- 반드시 O(1)의 추가 공간 복잡도와 O(n)의 시간 복잡도로 문제를 풀어야 한다.

2. head가 null이 아닌 경우만 3 ~ 5번을 수행한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- odd는 홀수번째 값을 ListNode로 저장할 변수로, head로 초기화한다.
- even은 짝수번쨰 값을 ListNode로 저장할 변수로, head.next로 초기화한다.
- temp는 even을 이용하여 뒤로 미룰 값들을 ListNode로 저장할 변수로, even과 동일하게 head.next로 초기화한다.

4. even과 even.next ListNode들이 null이 아닌 경우, 아래를 수행한다.
- odd.next에 evne.next를 넣어준다.
- even.next에 even.next.next를 넣어준다.
- odd에 odd.next를 넣어준다.
- even에 evne.next를 넣어준다.

5. odd.next에 temp를 넣어 짝수번째 위치의 값들을 이어준다.

6. 짝수번째 값들을 뒤로 이동시킨 head를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OddEvenLinkedList.java){:target="_blank"}에서 확인 가능합니다.