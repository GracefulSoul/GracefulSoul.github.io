---
title: "Leetcode Java Remove Nth Node From End of List"
excerpt: "Leetcode Remove Nth Node From End of List Java 풀이"
last_modified_at: 2021-04-29T23:50:00
header:
  image: /assets/images/leetcode/remove-nth-node-from-end-of-list.png
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
[Link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/){:target="_blank"}

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

  public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode result = new ListNode(0, head);
    ListNode pointer = result;
    ListNode temp = result;
    for (int i = 0; i <= n; i++) {
      pointer = pointer.next;
    }
    while (pointer != null) {
      temp = temp.next;
      pointer = pointer.next;
    }
    temp.next = temp.next.next;
    return result.next;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/486695652/){:target="_blank"}

# 설명
1. 특정 노드의 값을 제거한 ListNode를 만들 result 변수를 next 값에 head를 넣고 생성한다.
- 테스트 파라미터가 ListNode(1, null), 1을 주어진 경우 해당 노드를 삭제해야 하기 때문에 문제를 수행하기위해 임의의 값과 주어진 문제의 ListNode를 이용하여 껍데기 역할인 ListNode(0, head)로 선언한다.

2. 제거할 목표 노드의 위치를 탐색하기 위해 pointer와 temp를 result를 주입하여 만들어준다.

3. pointer는 주어진 정수 n번만큼 next값을 pointer에 주입하여 위치를 탐색하기 위한 초석을 만든다.
- 주어진 정수 n은 제거할 목표 노드의 역순 위치를 제공하므로, pointer를 먼저 이동하여 temp 노드가 제거할 목표의 위치까지 도달하기 위한 역할을 수행한다.

4. pointer가 null이 아닐 때 까지 반복을 수행하여 temp의 위치를 이동한다.
- 2번의 설명에 덧붙여서, 제거할 목표의 위치 전 노드의 위치로 이동을 해야 next 값에 next.next 값으로 넣어 줄 수 있으므로 주어진 정수 n번만큼 pointer를 이동시킨 것이다.
- 주어진 예제를 이용하여 설명하자면, "1 - 2 - 3(목표위치) - 4 - 5" 이 위치로 이동시키는 것이다.

5. 목표 위치의 전 노드에 도달한 temp의 next 값에, temp.next.next 값을 주입한다.
- 변수 temp는 변수 result를 참조하여 만들었으므로, 특정 ListNode의 값이 변경되면 result 또한 해당 노드의 값이 동일하게 변경된다.

6. 껍데기로 사용했던 변수 result 대신 변수 result의 next를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveNthNodeFromEndOfList.java){:target="_blank"}에서 확인 가능합니다.