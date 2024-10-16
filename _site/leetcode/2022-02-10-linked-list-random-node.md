---
title: "Leetcode Java Linked List Random Node"
excerpt: "Leetcode Linked List Random Node Java 풀이"
last_modified_at: 2022-02-10T13:00:00
header:
  image: /assets/images/leetcode/linked-list-random-node.png
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
[Link](https://leetcode.com/problems/linked-list-random-node/){:target="_blank"}

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

  private ListNode listNode;
  private int size;
  private Random random;

  public Solution(ListNode head) {
    this.listNode = head;
    this.size = 0;
    ListNode curr = head;
    while (curr != null) {
      this.size++;
      curr = curr.next;
    }
    this.random = new Random();
  }

  public int getRandom() {
    int num = this.random.nextInt(this.size);
    ListNode curr = this.listNode;
    while (num > 0) {
      curr = curr.next;
      num--;
    }
    return curr.val;
  }

}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(head);
 * int param_1 = obj.getRandom();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/638387842/){:target="_blank"}

# 설명
1. 단일 ListNode가 주어지면, 임의의 노드 값을 동일 확률로 반환하는 Solution 클래스를 완성하는 문제이다.
- 생성자인 Solution(ListNode head)은 Solution 객체에 head 넣어 초기화하는 역할을 수행한다.
- 메서드인 getRandom()는 Solution 객체에 주입된 ListNode 내 존재하는 값들을 동일한 확률로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- listNode는 생성자를 통해 주입된 ListNode를 저장하기 위한 변수이다.
- size는 listNode의 개수를 저장할 변수이다.
- random은 객체 내 존재하는 값을 임의 확률로 반환하기 위한 객체이다.

3. 생성자인 Solution(ListNode head)을 완성한다.
- 주입된 head를 listNoad에 넣어준다.
- size를 0으로 초기화 한다.
- curr에 head을 임시로 넣어주고 curr이 null이 아닐 때까지 반복을 수행하여 size에 node의 개수를 넣어준다.
- random에 Random 객체로 초기화 시켜준다.

4. 메서드인 getRandom()을 완성한다.
- num에 size 미만의 임의 숫자를 넣어준다.
  - [Random 객체의 nextInt(int bound) 메서드](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html#nextInt-int-){:target="_blank"}는 0부터 bound 미만까지의 임의 정수 숫자열을 반환한다.
- curr에 listNode를 넣고 num이 0 이상일 때 까지 이동하며 num번째 노드를 찾아준다.
- num번째 노드인 curr의 val 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/object/solution/random/node/Solution.java){:target="_blank"}에서 확인 가능합니다.