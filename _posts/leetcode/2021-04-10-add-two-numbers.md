---
title: "Leetcode Java Add Two Numbers"
excerpt: "Leetcode Add Two Numbers Java 풀이"
last_modified_at: 2021-04-09T18:00:00
header:
  image: /assets/images/leetcode/add-two-numbers.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://leetcode.com/problems/add-two-numbers/)

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

  public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode listNode = new ListNode();
    ListNode temp = listNode;
    int quotient = 0;
    while (l1 != null || l2 != null) {
      int sum = quotient + getValue(l1) + getValue(l2);
      quotient = sum / 10;
      temp.next = new ListNode(sum % 10);
      temp = temp.next;
      l1 = getNext(l1);
      l2 = getNext(l2);
    }
    if (quotient > 0) {
      temp.next = new ListNode(quotient);
    }
    return listNode.next;
  }
  
  private int getValue(ListNode listNode) {
    return listNode != null ? listNode.val : 0;
  }
  
  private ListNode getNext(ListNode listNode) {
    return listNode != null ? listNode.next : null;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/478103072/)

# 설명
1. ListNode를 먼저 파악해보면 숫자를 val 변수로 저장하고,다음 ListNode를 next 변수로 저장한다.
  - Java에서 [LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)를 이해하면 도움이 된다.
  - 하나의 ListNode는 숫자의 역순으로 저장이 되므로 val의 값은 1의 자리, 다음 ListNode의 val의 값은 10의 자리이다.
  - 예를 들어 숫자 123은 '3 - 2 - 1' 순의 ListNode로 구성된다.
  - 위의 경우 첫 ListNode의 val값은 3이고, next ListNode의 val값은 2이고, next ListNode의 val값은 1이며 next는 null이 된다.

2. 두 ListNode 값의 합을 더해야 하므로, 결과로 반환하기 위해 사용될 ListNode와 임시 ListNode를 구성할 listNode와 temp 변수를 선언한다.
  - listNode 변수는 결과 값을 누적하기 위해 사용된다.
  - temp 변수는 앞으로 계산할 val값을 지정하고, listNode의 next값을 지속적으로 넣어주기 위해 사용된다.

3. 주어진 두 ListNode의 val값을 차례대로 합산한다.
  - 한 자리는 0 ~ 9 까지 구성되므로 두 합은 최대 18이고, 이전 값을 10으로 나눈 몫을 합쳐도 두 자릿수이므로 현재 값에서 10으로 나눈 몫은 다음 값 계산에만 사용하면 된다.
  - 두 값의 합이 10을 초과할 시, 다음 ListNode의 val값을 계산할 때 사용하기 위해 quotient 변수에 10으로 나눈 몫을 임시 저장한다.
  - 현재 ListNode의 val은 이전에 10으로 나눈 몫인 quotient와 두 ListNode의 val값을 합쳐서 정한다.
  - 현재 ListNode의 next는 다시 temp에 할당하고, 주어진 두 ListNode는 next ListNode 값으로 재 할당한다.

4. 3번의 반복이 끝난 이후 몫이 남아있다면, temp의 next ListNode 값으로 넣어준다.

5. 계산이 끝난 listNode의 next 값을 주어진 문제의 결과로 반환한다.
  - 초기 ListNode를 선언하고 temp가 next값부터 주입되었으므로, 첫 ListNode는 껍데기이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TwoSum.java)에서 확인 가능합니다.