---
title: "Leetcode Java Partition List"
excerpt: "Leetcode Partition List Java 풀이"
last_modified_at: 2021-07-06T18:00:00
header:
  image: /assets/images/leetcode/partition-list.png
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
[Link](https://leetcode.com/problems/partition-list/){:target="_blank"}

# 코드
```java
class Solution {

  public ListNode partition(ListNode head, int x) {
    ListNode result = new ListNode(0, head);
    ListNode temp = result;
    ListNode pointer = result;
    while (pointer.next != null) {
      if (pointer.next.val < x) {
        if (pointer == temp) {
          pointer = pointer.next;
        } else if (temp.next != null && pointer.next != null) {
          this.swap(temp, pointer);
        }
        temp = temp.next;
      } else {
        pointer = pointer.next;
      }
    }
    return result.next;
  }

  private void swap(ListNode ln1, ListNode ln2) {
    ListNode temp = ln2.next;
    ln2.next = temp.next;
    temp.next = ln1.next;
    ln1.next = temp;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/518055175/){:target="_blank"}

# 설명
1. 주어진 ListNode인 head의 내부 값들 중 주어진 정수 x보다 큰 값이 존재할 경우, 순서를 마지막으로 미루어 x보다 작은 값들을 우선 배치하고 그 이후 해당 값들을 주어진 순서대로 배치하는 문제이다.

2. 주어진 문제를 풀기 위해 변수를 정의한다.
- 결과를 만들기 위한 변수인 result에 주어진 변수 head를 이용하여 new ListNode(0, head)를 넣어준다.
- 값의 위치를 변경하기 위한 임시 변수인 temp와 주어진 정수 x보다 큰 값을 찾기 위한 pointer 변수에 result를 각각 주입해준다.

3. pointer.next가 null이 아닐 때 까지 반복하여 주어진 정수 x보다 큰 값을 후순위로 미루어 값을 정렬해준다.
- pointer.next.val의 값이 x보다 작은 경우 값을 확인한다.
  - pointer와 temp가 동일한 경우 pointer의 위치가 temp와 동일하므로, pointer를 다음 ListNode로 이동시킨다.
  - temp.next와 pointer.next가 존재하는 경우, 각 next의 객체를 바꾸어준다.
    - pointer.next와 temp.next를 각각 바꾸어 순서를 변경한다.
  - temp를 다음 ListNode로 이동시킨다.
- pointer.next.val의 값이 x보다 크거나 같은 경우, pointer를 다음 ListNode로 이동시킨다.

4. 반복이 완료되면 껍데기로 감싸 넣었던 변수 result의 next 객체를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PartitionList.java){:target="_blank"}에서 확인 가능합니다.