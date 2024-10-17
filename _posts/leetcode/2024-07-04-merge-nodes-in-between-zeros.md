---
title: "Leetcode Java Merge Nodes in Between Zeros"
excerpt: "Leetcode Medium - 'Merge Nodes in Between Zeros' 문제 Java 풀이"
last_modified_at: 2024-07-04T18:40:00
header:
  image: /assets/images/leetcode/merge-nodes-in-between-zeros.png
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
[Link](https://leetcode.com/problems/merge-nodes-in-between-zeros/){:target="_blank"}

# 코드
```java
class Solution {

  public ListNode mergeNodes(ListNode head) {
    ListNode temp = head.next;
    ListNode next = temp;
    while (next != null) {
      int sum = 0;
      while (next.val != 0) {
        sum += next.val;
        next = next.next;
      }
      temp.val = sum;
      next = next.next;
      temp.next = next;
      temp = temp.next;
    }
    return head.next;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/merge-nodes-in-between-zeros/submissions/1309222219/){:target="_blank"}

# 설명
1. head에서 노드의 값이 0인 노드들 사이의 값을 하나의 노드의 값으로 합쳐서 하나의 리스트 노드로 반환하는 문제이다.

2. temp와 next는 노드를 이동하며 하나의 리스트 노드로 값을 합치기 위한 변수로, 둘 다 처음 값이 0인 노드를 제외한 head의 다음 노드로 초기화한다.

3. next 노드가 null이 아닐 때 까지 아래를 반복한다.
- sum은 0이 아닌 노드의 값을 합치기 위한 변수로, 0으로 초기화한다.
- next 노드의 val 값이 0이 아닐 때 까지, next의 값을 더한 후 next에 next의 다음 노드를 넣어준다.
- temp의 val의 값에 sum을 넣어 합계를 넣어준다.
- next에 next의 다음 노드를 넣어, 값이 0인 노드를 넘어간다.
- temp의 다음 노드에 next로 넣어준 후, temp에는 temp의 다음 노드를 넣어준다.

4. 반복이 완료되면 temp를 통해 하나의 리스트 노드로 만든 head의 next 리스트 노드를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MergeNodesInBetweenZeros.java){:target="_blank"}에서 확인 가능합니다.