---
title: "Leetcode Java Delete Nodes From Linked List Present in Array"
excerpt: "Leetcode Delete Nodes From Linked List Present in Array Java"
last_modified_at: 2024-09-06T18:40:00
header:
  image: /assets/images/leetcode/delete-nodes-from-linked-list-present-in-array.png
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
[Link](https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array/){:target="_blank"}

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

  public ListNode modifiedList(int[] nums, ListNode head) {
    int max = -1;
    for (int num : nums) {
      max = num > max ? num : max;
    }
    boolean[] frequency = new boolean[max + 1];
    for (int num : nums) {
      frequency[num] = true;
    }
    ListNode temp = new ListNode();
    ListNode curr = temp;
    while (head != null) {
      if (head.val > max || frequency[head.val] == false) {
        curr.next = head;
        curr = curr.next;
      }
      head = head.next;
    }
    curr.next = null;
    return temp.next;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array/submissions/1380913842/){:target="_blank"}

# 설명
1. head에서 nums 내 값들을 제거하고 반환하는 문제이다.

2. 문제 풀이에 필요한 변수이다.
- max는 nums 내 가장 큰 값을 저장한 변수이다.
- frequency는 nums 내 값의 존재 유무를 저장할 배열로, $max + 1$ 크기의 배열로 초기화하여 nums의 값 위치에 true를 넣어준다.
- temp는 결과를 임시 저장할 변수로, 새 ListNode로 초기화한다.
- curr은 현재 노드를 저장할 변수로 temp로 초기화한다.

3. head가 null이 아닐 때 까지 아래를 반복한다.
- haed의 val 값이 max보다 크거나 frequency에 존재하지 않는 경우, curr의 next에 head를 넣고 curr에 curr의 next 노드를 넣어 현재 노드를 제거해준다.
- head에 haed의 next 노드를 넣어 다음 반복을 수행한다.

4. curr의 next 노드를 null로 바꾸어 마지막 노드로 만든 후, temp의 next 노드인 제거된 노드를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteNodesFromLinkedListPresentInArray.java){:target="_blank"}에서 확인 가능합니다.