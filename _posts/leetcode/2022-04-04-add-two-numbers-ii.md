---
title: "Leetcode Java Add Two Numbers II"
excerpt: "Leetcode Add Two Numbers II Java 풀이"
last_modified_at: 2022-04-04T18:00:00
header:
  image: /assets/images/leetcode/add-two-numbers-ii.png
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
[Link](https://leetcode.com/problems/add-two-numbers-ii/){:target="_blank"}

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
    l1 = this.reverseList(l1);
    l2 = this.reverseList(l2);
    ListNode result = null;
    ListNode temp = result;
    int carry = 0;
    while (l1 != null && l2 != null) {
      int sum = carry + l1.val + l2.val;
      carry = sum / 10;
      ListNode listNode = new ListNode(sum % 10);
      if (result == null) {
        result = listNode;
        temp = result;
      } else {
        temp.next = listNode;
        temp = temp.next;
      }
      l1 = l1.next;
      l2 = l2.next;
    }
    while (l1 != null) {
      int sum = carry + l1.val;
      carry = sum / 10;
      temp.next = new ListNode(sum % 10);
      l1 = l1.next;
      temp = temp.next;
    }
    while (l2 != null) {
      int sum = carry + l2.val;
      carry = sum / 10;
      temp.next = new ListNode(sum % 10);
      l2 = l2.next;
      temp = temp.next;
    }
    while (carry != 0) {
      temp.next = new ListNode(carry % 10);
      carry /= 10;
      temp = temp.next;
    }
    return this.reverseList(result);
  }

  private ListNode reverseList(ListNode ls) {
    ListNode reverse = new ListNode(ls.val);
    while (ls.next != null) {
      ls = ls.next;
      reverse = new ListNode(ls.val, reverse);
    }
    return reverse;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/673560144/){:target="_blank"}

# 설명
1. 숫자를 ListNode로 만든 l1과 l2를 이용하여 합친 값으로 새 ListNode를 만들어 반환하는 문제이다.

2. ListNode의 값들을 역순으로 전환하기 위한 reverseList(ListNode ls) 메서드를 정의한다.
- ls의 val 값으로 ListNode를 만들어서 reverse에 정의하고, ls의 next가 null이 아닐 때 까지 반복하여 reverse에 ls 내 val 값들을 역순으로 만들어준다.
- 반복이 완료되면 reverse를 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- l1과 l2에 2번에서 정의한 reverseList(ListNode ls) 메서드를 이용하여 값들을 역순으로 만들어준다.
- result는 결과를 넣을 변수로, null로 초기화한다.
- temp는 결과를 엮어줄 임시 변수로, result로 초기화한다.
- carry는 숫자의 합이 10 이상일 경우, 10 자릿수를 넣어줄 변수이다.

4. l1과 l2가 null이 아닐 때 까지 반복하여 아래를 수행한다.
- sum에 l1과 l2의 val 값과 carry의 합을 넣어준다.
- carry에 10을 나눈 값을 carry에 다시 넣어준다.
- listNode에 sum의 1 자릿수를 이용하여 새 ListNode를 만들어 넣어준다.
- result가 null인 경우 첫 값이므로, result에 listNode와 temp에 result를 넣어준다.
- result가 null이 아니면, temp의 next에 ListNode를 temp에 temp의 next ListNode를 넣어준다.
- l1에 l1의 next ListNode를 l2에 l2의 next ListNode를 넣어준다.

5. l1, l2 순으로 각 ListNode가 null이 아닐 때 까지 반복하여 아래를 수행한다.
- sum에 carry와 val 값을 더해준다.
- carry에 10을 나눈 값을 carry에 다시 넣어준다.
- temp의 next에 sum의 1 자릿수를 이용하여 새 ListNode를 만들어 넣어준다.
- l1에 l1의 next ListNode를, temp에 temp의 next ListNode를 넣어준다.

6. carry에 값이 남아있는 경우, 아래를 수행한다.
- temp의 next ListNode에 carry의 1 자릿수를 이용하여 새 ListNode를 만들어 넣어준다.
- carry에 10을 나눈 값을 carry에 다시 넣어준다.
- temp에 temp의 next ListNode를 넣어준다.

7. 역순의 값을 더해 이어준 result를 2번의 reverseList(ListNode ls) 메서드를 이용하여 다시 원래대로 돌려서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AddTwoNumbersII.java){:target="_blank"}에서 확인 가능합니다.