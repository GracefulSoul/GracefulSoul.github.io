---
title: "Leetcode Java Remove Duplicates from Sorted Array"
excerpt: "Leetcode Remove Duplicates from Sorted Array Java 풀이"
last_modified_at: 2021-05-08T18:10:00
header:
  image: /assets/images/leetcode/remove-duplicates-from-sorted-array.png
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
    int idx = 0;
    for (int n : nums) {
      if (idx == 0 || n > nums[idx - 1]) {
        nums[idx++] = n;
      }
    }
    return idx;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/490416459/){:target="_blank"}

# 설명
1. 주어진 배열 nums는 이미 정렬이 되어 있으므로, 배열 내 이전 index의 값이 다른 경우의 갯수만 확인하면 된다.
- 문제의 결과는 중복되지 않은 배열의 값의 갯수이므로, 새 배열을 선언하여 넣지 않아도 된다.
- 배열의 첫 값은 무조건 중복되지 않은 값이므로, count를 증가시킨다.
- 가장 중요한 idx 값을 점층적으로 증가시키면서 nums[idx++] 값에 중복되지 않은 값을 넣는 이유는, 중복되지 않은 값을 비교하면서 count를 세기 위함이다.

2. 반복이 종료되면, 중복되지 않은 값의 갯수를 저장하는 idx를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveDuplicatesfromSortedArray.java){:target="_blank"}에서 확인 가능합니다.