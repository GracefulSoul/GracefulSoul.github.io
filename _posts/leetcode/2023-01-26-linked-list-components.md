---
title: "Leetcode Java Linked List Components"
excerpt: "Leetcode - 'Linked List Components' 문제 Java 풀이"
last_modified_at: 2023-01-26T20:40:00
header:
  image: /assets/images/leetcode/linked-list-components.png
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
[Link](https://leetcode.com/problems/linked-list-components){:target="_blank"}

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

  public int numComponents(ListNode head, int[] nums) {
    int max = 0;
    for (int num : nums) {
      max = Math.max(max, num);
    }
    int[] dp = new int[max + 1];
    for (int num : nums) {
      dp[num]++;
    }
    int connected = 0;
    int result = 0;
    while (head != null) {
      if (head.val <= max && dp[head.val] == 1) {
        connected++;
      } else if (connected > 0) {
        result++;
        connected = 0;
      }
      head = head.next;
    }
    if (connected > 0) {
      result++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/linked-list-components/submissions/885618789/){:target="_blank"}

# 설명
1. head 내 nums에 포함된 노드들로 이어진 부분 ListNode의 개수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 nums 내 최대 값을 저장한다.
- dp는 nums의 숫자가 포함되었는지 저장할 배열로, 위의 max 크기로 초기화하여 nums를 반복하여 숫자가 존재하는 경우 해당 위치의 값을 증가시킨다.
- connected는 한 번에 연결되는 노드의 개수를 저장할 변수로, 0으로 초기화한다.
- result는 부분 ListNode의 개수를 저장할 변수로, 0으로 초기화한다.

3. head가 null이 아닐 때 까지 아래를 반복한다.
- head의 val 값이 max 이하이고 dp 내 앞의 값에 해당하는 위치의 값이 1인 경우, 연결된 노드의 연속이므로 connected를 증가시킨다.
- 위의 경우가 아니면서 connected가 0보다 큰 경우, 연결된 노드가 끝났으므로 result를 증가시키고 connected를 0으로 초기화한다.
- head에 head의 next ListNode를 넣어주고 반복을 계속한다.

4. 마지막으로 connected의 값이 0보다 큰 마지막 부분 ListNode가 존재하는 경우 result를 증가시킨다.

5. 부분 ListNode의 개수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LinkedListComponents.java){:target="_blank"}에서 확인 가능합니다.