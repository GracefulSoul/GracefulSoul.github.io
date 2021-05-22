---
title: "Leetcode Java Merge Two Sorted Lists"
excerpt: "Leetcode Merge Two Sorted Lists Java 풀이"
last_modified_at: 2021-05-01T17:30:00
header:
  image: /assets/images/leetcode/merge-two-sorted-lists.png
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

  public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
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
[Link](https://leetcode.com/submissions/detail/487337839/){:target="_blank"}

# 설명
1. 주어진 두 ListNode l1, l2가 정렬되어 있으므로, 순차적으로 각 val의 값을 비교하여 ListNode를 합쳐주면 된다.
- val 값이 작은 ListNode의 next의 ListNode와 다른 ListNode로 재귀호출이 수행된다.
- 한 ListNode의 next 값이 null이 되면 다른 ListNode의 모든 val 값은 마지막 비교한 상대 ListNode의 val 값보다 크므로 해당 ListNode를 반환한다.
- 이제 순차적으로 val 값이 작은 ListNode의 결과에 따라서 next 값에 재귀 호출 결과가 들어가게 된다.
- 이렇게 조건문이 수행된 역순으로 각 절차가 수행되게 되면, 마지막으로 수행된 값은 순서대로 두 ListNode를 합친 ListNode가 되어 주어진 문제의 결과로 반환된다.

# 예제
- 주어진 문제의 Example 1을 이용하여 작업 절차를 예제로 보여주겠다.

1. 각 ListNode의 초기 값은 l1 = [1, 2, 4] & l2 = [1, 2, 4]로, 재귀 호출이 반복되어 l1이 반환된다.
- l1 = 4, l2 = null
2. 마지막으로 수행된 재귀호출은 l1 = 4 & l2 = 4 이므로, l1 < l2를 만족하지 않아 l2.next에 l1이 들어가게 된다.
- l1 = 4, l2 = [4, 4]
3. 그 전의 경우는 l1 = 4 & l2 = 3 이므로, l1 < l2를 만족하지 않아 l2.next에 l2가 들어가게 된다.
- l1 = 4, l2 = [3, 4, 4]
4. 그 전의 경우는 l1 = 2 & l2 = 3 이므로, l1 < l2를 만족하여 l1.next에 l1이 들어가게 된다.
- l1 = [2, 3, 4, 4], l2 = [3, 4, 4]
5. 그 전의 경우는 l1 = 1 & l2 = 3 이므로, l1 < l2를 만족하여 l1.next에 l1이 들어가게 된다.
- l1 = [1, 2, 3, 4, 4], l2 = [3, 4, 4]
6. 최초 재귀 호출의 경우는 l1 = 1 & l2 = 1 이므로, l1 < l2를 만족하지 않아 l2.next에 l1이 들어가게 되어 l2가 주어진 문제의 결과로 반환된다.
- l1 = [1, 2, 3, 4, 4], l2 = [1, 1, 2, 3, 4, 4]

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MergeTwoSortedLists.java){:target="_blank"}에서 확인 가능합니다.