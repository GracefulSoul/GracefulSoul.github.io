---
title: "Leetcode Java Palindrome Linked List"
excerpt: "Leetcode - 'Palindrome Linked List' 문제 Java 풀이"
last_modified_at: 2021-11-10T12:00:00
header:
  image: /assets/images/leetcode/palindrome-linked-list.png
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
[Link](https://leetcode.com/problems/palindrome-linked-list/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isPalindrome(ListNode head) {
    ListNode fast = head;
    ListNode slow = head;
    ListNode prev = null;
    while (fast != null && fast.next != null) {
      fast = fast.next.next;
      ListNode temp = prev;
      prev = slow;
      slow = slow.next;
      prev.next = temp;
    }
    if (fast != null) {
      slow = slow.next;
    }
    while (prev != null && prev.val == slow.val) {
      slow = slow.next;
      prev = prev.next;
    }
    return prev == null;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/584758469/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head의 val 값들이 앞뒤로 읽어도 같은 문자열(이하 회문)이 되는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- fast와 slow는 주어진 노드 head의 중간 지점을 탐색하기 위한 ListNode로, head를 각각 넣어 초기화한다.
- prev는 주어진 노드 head의 처음부터 중간 지점까지 값들을 반전시켜 저장할 ListNode로, null로 초기화 한다.

3. fast와 fast.next가 null이 아닐 때 까지 반복하여 아래를 수행한다.
- fast에 fast.next.next ListNode를 넣어 두 개의 ListNode를 이동시킨다.
- temp에 지금까지 반전시킨 ListNode인 prev를 넣어 임시 보관한다.
- prev에 slow의 ListNode를 넣어 현재 위치의 ListNode를 넣어준다.
- slow는 slow.next를 넣어 fast의 위치보다 $\frac{1}{2}$ 지점에 위치하게 하여 head의 중간 지점에 위치하도록 유도한다.
- prev.next에 temp를 다시 넣어주어 slow까지 진행된 ListNode를 반전시킨 값을 유지한다.

4. fast가 null이 아닌 경우 ListNode가 홀수로 존재한다는 의미이므로, 회문의 중앙값에 위치한 slow에 다음 위치로 이동시키기 위해 slow.next를 넣어 다음 위치부터 회문 검증을 수행하도록 한다.
- 예를 들어 1,2,3,2,1 인 경우, 아래와 같다.
  - fast는 <s>1,2,3,2,</s><b>1</b> 에 위치한다.
  - slow는 <s>1,2,</s><b>3</b>,2,1에 위치한다.
  - prev는 2,1의 값들이 존재한다.
  - slow와 prev를 검증하기 위해 slow에 다음 ListNode인 slow.next를 넣어 <s>1,2,3,</s><b>2</b>,1에 위치시키도록 하여 회문의 중심이 되는 3을 기준으로 검증을 수행할 수 있도록 한다.

5. prev가 null이 아니고, prev.val의 값과 slow.val 값이 동일할 때 까지 반복하여 slow와 prev에 next ListNode들을 각각 넣어준다.

6. prev가 null인 경우 5번의 검증을 통해 회문인 ListNode로 판단되므로 true를, 아닌 경우 회문인 ListNode가 아니므로 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PalindromeLinkedList.java){:target="_blank"}에서 확인 가능합니다.