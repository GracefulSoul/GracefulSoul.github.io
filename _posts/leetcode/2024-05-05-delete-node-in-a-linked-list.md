---
title: "Leetcode Java Delete Node in a Linked List"
excerpt: "Leetcode Delete Node in a Linked List Java"
last_modified_at: 2024-05-05T20:50:00
header:
  image: /assets/images/leetcode/delete-node-in-a-linked-list.png
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
[Link](https://leetcode.com/problems/delete-node-in-a-linked-list/){:target="_blank"}

# 코드
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {

	public void deleteNode(ListNode node) {
		node.val = node.next.val;
		node.next = node.next.next;
	}

}
```

# 결과
[Link](https://leetcode.com/problems/delete-node-in-a-linked-list/submissions/1249968317/){:target="_blank"}

# 설명
1. ListNode로 이루어진 노드들 중 주어진 node만 제거하는 문제이다.

2. node의 현재 값에 다음 노드의 값을 넣고, 다음 노드를 다다음 노드로 연결시켜 현재 노드를 제거해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteNodeInALinkedList.java){:target="_blank"}에서 확인 가능합니다.