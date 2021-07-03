---
title: "Leetcode Java Remove Duplicates from Sorted List II"
excerpt: "Leetcode Remove Duplicates from Sorted List II Java 풀이"
last_modified_at: 2021-07-01T12:40:00
header:
  image: /assets/images/leetcode/remove-duplicates-from-sorted-list-ii.png
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
[Link](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public ListNode deleteDuplicates(ListNode head) {
    return this.recursive(head, null);
  }

  private ListNode recursive(ListNode head, ListNode previous) {
    if (head == null) {
      return null;
    } else {
      if ((head.next != null && head.val == head.next.val) || (previous != null && head.val == previous.val)) {
        return this.recursive(head.next, head);
      } else {
        head.next = this.recursive(head.next, head);
        return head;
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/515857149/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head의 val 값이 중복된 ListNode를 모두 제거하고 중복되지 않은 값들을 가진 ListNode를 반환하는 문제이다.

2. 재귀 호출을 통해서 head와 이전의 값을 privious 변수에 넣어 중복된 ListNode들을 제외하고 역순으로 ListNode를 만들어 주어진 문제의 결과로 반환한다.
- head가 null인 경우, 주어진 ListNode인 head의 마지막 값이므로 그대로 반환한다.
- head가 null이 아닌 경우, 아래의 경우를 확인하여 중복을 제거한 값을 찾기 위해서 재귀 호출을 반복한다.
  - head.next가 존재하고, head.val 값과 head.next의 val 값이 동일하면 현재 값과 다음 값이 동일한 경우이다.
  - previous가 존재하고 head.val 값과 privious.val 값이 동일하면 이전 값과 현재 값이 동일한 경우이다.
  - 위 두 경우는 중복된 값이 존재하므로 무시하고 재귀 호출의 값을 반환한다.
  - 위 두 경우가 아니면 중복된 값이 존재하지 않으므로 head.next에 해당 재귀 호출의 값을 넣고 head를 반환한다.
- 재귀 호출을 통해 역순으로 중복이 제거되어 만들어진 ListNode를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveDuplicatesFromSortedListII.java){:target="_blank"}에서 확인 가능합니다.