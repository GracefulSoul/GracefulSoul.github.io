---
title: "Leetcode Java Intersection of Two Linked Lists"
excerpt: "Leetcode Intersection of Two Linked Lists Java 풀이"
last_modified_at: 2021-09-13T13:00:00
header:
  image: /assets/images/leetcode/intersection-of-two-linked-lists.png
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
[Link](https://leetcode.com/problems/intersection-of-two-linked-lists/){:target="_blank"}

# 코드
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {

  public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    if (headA == null || headB == null) {
      return null;
    }
    ListNode listNodeA = headA;
    ListNode listNodeB = headB;
    while (listNodeA != listNodeB) {
      listNodeA = listNodeA == null ? headB : listNodeA.next;
      listNodeB = listNodeB == null ? headA : listNodeB.next;
    }
    return listNodeA;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/553983942/){:target="_blank"}

# 설명
1. 주어진 ListNode headA와 headB를 이용하여 공통된 부분 ListNode를 찾는 문제이다.
- 공통된 부분 ListNode가 없을 경우, null을 주어진 문제의 결과로 반환한다.

2. headA 혹은 headB가 null인 경우, 공통된 부분이 없기 때문에 null을 주어진 문제의 결과로 반환한다.

3. 임시 변수 listNodeA에는 headA를, listNodeB에는 headB를 넣어 정의한다.

4. listNodeA와 listNodeB가 같지 않을 때 까지 반복하여 공통된 부분 ListNode를 찾는다.
- listNodeA가 null인 경우, headB를 listNodeA에 넣어 공통된 부분 ListNode를 찾는다.
- listNodeA가 null이 아닌 경우, listNodeA.next를 listNodeA에 넣어 다음 ListNode로 이동시킨다.
- listNodeB가 null인 경우, headA를 listNodeB에 넣어 공통된 부분 ListNode를 찾는다.
- listNodeB가 null이 아닌 경우, listNodeB.next를 listNodeA에 넣어 다음 ListNode로 이동시킨다.
  - listNodeA와 listNodeB의 길이가 다른 경우 서로 전환하여 수행하면 같은 길이가 되므로 탐색이 가능하다.
  - 예를 들어, 1 -> 2 -> 3 -> 4 & 5 -> 3 -> 4 두 ListNode가 있다고 할 때 아래와 같이 수행되면서 공통된 부분 ListNode를 탐색하게 된다.
    - listNodeA : 1 -> 2 -> 3 -> 4 -> (null)5 -> <b>3 -> 4 -> null</b>
    - listNodeB : 5 -> 3 -> 4 -> (null)1 -> 2 -> <b>3 -> 4 -> null</b>
  - 예를 들어, 1 -> 2 -> 3 & 4 -> 5 두 ListNode가 있다고 할 때 아래와 같이 수행되면서 공통된 부분 ListNode를 탐색하게 된다.
    - listNodeA : 1 -> 2 -> 3 -> (null)4 -> 5 -> <b>null</b>
    - listNodeB : 4 -> 5 -> (null)1 -> 2 -> 3 -> <b>null</b>

5. 위의 반복이 종료되면 공통된 부분으로 구성된 listNodeA와 listNodeB 둘 중 아무 ListNode를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinStack.java){:target="_blank"}에서 확인 가능합니다.