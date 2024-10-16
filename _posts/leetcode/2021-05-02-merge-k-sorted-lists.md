---
title: "Leetcode Java Merge k Sorted Lists"
excerpt: "Leetcode Merge k Sorted Lists Java 풀이"
last_modified_at: 2021-05-02T12:40:00
header:
  image: /assets/images/leetcode/merge-k-sorted-lists.png
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
[Link](https://leetcode.com/problems/merge-two-sorted-lists/){:target="_blank"}

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

  public ListNode mergeKLists(ListNode[] lists) {
    return this.mergeListsRecursion(lists, 0, lists.length - 1);
  }

  private ListNode mergeListsRecursion(ListNode[] lists, int start, int end) {
    if (start == end) {
      return lists[start];
    } else if (start < end) {
      int half = (start + end) / 2;
      ListNode l1 = this.mergeListsRecursion(lists, start, half);
      ListNode l2 = this.mergeListsRecursion(lists, half + 1, end);
      return this.mergeTwoLists(l1, l2);
    } else {
      return null;
    }
  }

  private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if (l1 == null) {
      return l2;
    } else if (l2 == null) {
      return l1;
    } else {
      if (l1.val < l2.val) {
        l1.next = mergeTwoLists(l1.next, l2);
        return l1;
      } else {
        l2.next = mergeTwoLists(l1, l2.next);
        return l2;
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/487716457/){:target="_blank"}

# 설명
1. 주어진 ListNode의 배열을 절반으로 나누어 각각을 재귀호출을 통해서 ListNode를 합친다.
- 재귀 호출은 주어진 배열의 index가 0에서 $lists.length - 1$까지의 ListNode를 합쳐야 하므로, 해당 값으로 변수 start와 end로 해당 값을 받아 재귀 호출을 수행하도록 한다.

2. 만일 변수 start의 값과 end의 값이 동일한 경우에는 ListNode를 합칠 이유가 없으므로, 주어진 배열 lists의 변수 start의 값의 ListNode를 반환한다.
- start와 end의 값이 동일하므로, end의 값을 사용해도 된다.

3. 만일 변수 start의 값이 end보다 작을 경우만 아래의 작업을 수행하고, 그 외는 초기 값인 null을 반환한다.
- 주어진 배열 lists를 절반으로 분할하여 ListNode를 하나로 합치기 위해서 half 변수를 $\frac{start - end}{2}$의 값으로 초기화한다.
- ListNode l1은 end 파라미터 자리에 half를 사용하여 재귀호출을 수행한 결과를 저장한다.
- ListNode l2는 start 파라미터 자리에 $half + 1$을 사용하여 재귀호출을 수행한 결과를 저장한다.
- 각 재귀호출의 결과를 저장한 ListNode l1과 l2를 이전에 작성하였던 [Merge Two Sorted Lists](../merge-two-sorted-lists/)를 활용하여 하나의 ListNode로 합쳐준다.

4. 재귀호출이 끝난 ListNode를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MergeKSortedLists.java){:target="_blank"}에서 확인 가능합니다.