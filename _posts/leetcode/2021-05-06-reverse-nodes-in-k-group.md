---
title: "Leetcode Java Reverse Nodes in k-Group"
excerpt: "Leetcode Reverse Nodes in k-Group Java 풀이"
last_modified_at: 2021-05-06T18:10:00
header:
  image: /assets/images/leetcode/reverse-nodes-in-k-group.png
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
[Link](https://leetcode.com/problems/reverse-nodes-in-k-group/){:target="_blank"}

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

  public ListNode reverseKGroup(ListNode head, int k) {
    ListNode curr = head;
    int count = 0;
    while (curr != null && count != k) {
      curr = curr.next;
      count++;
    }
    if (count == k) {
      curr = this.reverseKGroup(curr, k);
      while (count-- > 0) {
        ListNode tmp = head.next;
        head.next = curr;
        curr = head;
        head = tmp;
      }
      head = curr;
    }
    return head;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/489565583/){:target="_blank"}

# 설명
1. 특정 위치까지 숫자를 반전시키기 위해 주어진 ListNode head를 변수 curr에 넣고, 변수 count를 0으로 정의한다.

2. ListNode curr이 null이 아니거나 count가 k보다 작을 때 까지 반복을 통해 ListNode를 이동한다.
- 이동시킨 ListNode curr은 반전시킬 위치 이후($k + 1$)의 위치까지 이동시켜, 이전 노드들을 반전시킬 수 있도록 한다.
- count를 증가시켜, 반전시켜야 할 ListNode의 개수를 파악한다.

3. count와 k가 동일하면, 재귀 호출을 이용하여 k 배수만큼의 숫자를 반전시킨다.
- 2번 에서 $k + 1$까지 이동시킨 curr를 이용하여 재귀호출을 통해 다시 k자릿수가 될 경우, 반전시키고 그렇지 않은 경우 curr을 그대로 반환한다.
- 반전시키기 위해서 tmp 변수를 선언하여 ListNode의 순서를 역순으로 넣어준다.

4. 반복을 통해 반전시킨 ListNode curr을 head에 넣고, 주어진 문제의 결과로 반환한다.
- 재귀 호출의 경우, k 배수가 안될 경우 주어진 head를 그대로 반환하기 위해서 반환의 기준을 head로 한다.
- 재귀 호출로 반복되는 경우, k 배수만큼 숫자를 반복으로 반전시킨다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseNodesInKGroup.java){:target="_blank"}에서 확인 가능합니다.