---
title: "Leetcode Java Next Greater Node In Linked List"
excerpt: "Leetcode Medium - 'Next Greater Node In Linked List' 문제 Java 풀이"
last_modified_at: 2024-01-07T10:20:00
header:
  image: /assets/images/leetcode/next-greater-node-in-linked-list.png
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
[Link](https://leetcode.com/problems/next-greater-node-in-linked-list){:target="_blank"}

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

  public int[] nextLargerNodes(ListNode head) {
    List<Integer> list = new ArrayList<>();
    for (ListNode node = head; node != null; node = node.next) {
      list.add(node.val);
    }
    int[] result = new int[list.size()];
    Stack<Integer> stack = new Stack<>();
    for (int i = 0; i < list.size(); i++) {
      while (!stack.isEmpty() && list.get(stack.peek()) < list.get(i)) {
        result[stack.pop()] = list.get(i);
      }
      stack.push(i);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/next-greater-node-in-linked-list/submissions/1139003859/){:target="_blank"}

# 설명
1. head의 각 노드에서 우측에 있는 값들 중 현재 값보다 가장 큰 값을 찾아 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- list는 각 노드의 값들을 넣어줄 변수로, ArrayList로 정의하고 node의 val 값을 순차적으로 넣어준다.
- result는 결과를 넣을 변수로, list의 크기의 정수 배열로 초기화한다.
- stack은 노드 별 각 값을 비교하고 넣을 변수로, Stack으로 초기화한다.

3. 0부터 list의 길이 미만까지 i를 증가시키면서 아래를 수행한다.
- stack이 비어있지 않으면서 list에서 stack의 가장 나중에 넣은 값에 해당하는 위치의 값이 list의 i번째 값보다 작은 경우, result의 stack 내 앞의 값을 꺼내 해당하는 위치에 list의 i번째 값을 넣어준다.
- 값의 비교를 위해 stack에 i를 넣어준다.

4. 반복이 완료되면 각 노드 별 비교 값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NextGreaterNodeInLinkedList.java){:target="_blank"}에서 확인 가능합니다.