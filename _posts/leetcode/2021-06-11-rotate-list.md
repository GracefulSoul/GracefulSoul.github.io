---
title: "Leetcode Java Rotate List"
excerpt: "Leetcode Rotate List Java 풀이"
last_modified_at: 2021-06-11T22:10:00
header:
  image: /assets/images/leetcode/rotate-list.png
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
[Link](https://leetcode.com/problems/rotate-list/){:target="_blank"}

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

  public ListNode rotateRight(ListNode head, int k) {
    if (head == null || k == 0) {
      return head;
    }
    ListNode temp = head;
    int size = 1;
    while (temp.next != null) {
      temp = temp.next;
      size++;
    }
    temp.next = head;
    for (int idx = 0; idx < size - (k % size); idx++) {
      temp = temp.next;
    }
    head = temp.next;
    temp.next = null;
    return head;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/506375322/){:target="_blank"}

# 설명
1. 주어진 ListNode head를 k번 오른쪽으로 이동시킨 결과를 반환하는 문제이다.

2. 아래의 두 경우에는 이동시키는 의미가 없으므로, 주어진 문제의 결과로 head를 그대로 반환한다.
- 주어진 head가 null일 경우, 이동시킬 값이 없으므로 의미가 없다.
- 주어진 k가 0일 경우, 이동시키지 않으므로 의미가 없다.

3. 임시 ListNode temp를 head로 초기화 하고, 크기를 파악하기 위한 size 변수를 1로 초기화하여 선언한다.

4. temp.next가 null이 아닐 경우까지 반복하여 주어진 ListNode head의 size를 측정한다.

5. temp.next에 head를 주입하고, $size - (k \mod size)$만큼 반복하여 시작 위치를 이동시킨다.
- temp를 head로 초기화 하고, temp.next에 head를 주입함으로써 temp.next부터 head 객체들의 반복으로 구성이 된다.
  - 즉, temp의 값이 [5, null]에서 [5, [1, [2, [3, [4, [5, [1, [2, ...]]]]]]]] 이렇게 구성이 된다.
  - 그러므로 head가 반복 구성이 되므로, [1, [2, [3, [4, [5, x]]]]] 까지의 참조 값은 x부터 반복되는 객체들과 동일하다.
- temp에 temp.next값을 주입하여 시작되는 NodeList의 위치를 탐색한다.

6. head에 temp.next값을 넣어 시작되는 NodeList를 설정한다.

7. temp.next를 null로 주입하여 5번에서 설명한 반복 구성을 제거함으로써, 종료되는 NodeList를 설정한다.
- temp.next의 값을 null로 주입하면, head에서 반복된 값의 다음 반복이 시작되는 NodeList의 next 값을 null로 설정하여 객체의 반복 구성을 제거한다.

8. 6번과 7번을 통해 값이 정리된 head를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RotateList.java){:target="_blank"}에서 확인 가능합니다.