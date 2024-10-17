---
title: "Leetcode Java Copy List with Random Pointer"
excerpt: "Leetcode - 'Copy List with Random Pointer' 문제 Java 풀이"
last_modified_at: 2021-08-26T17:00:00
header:
  image: /assets/images/leetcode/copy-list-with-random-pointer.png
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
[Link](https://leetcode.com/problems/copy-list-with-random-pointer/){:target="_blank"}

# 코드
```java
class Solution {

  public Node copyRandomList(Node head) {
    return this.recursive(head, new HashMap<>());
  }

  private Node recursive(Node node, Map<Node, Node> map) {
    if (node == null) {
      return null;
    } else if (map.containsKey(node)) {
      return map.get(node);
    } else {
      Node temp = new Node(node.val);
      map.put(node, temp);
      temp.next = this.recursive(node.next, map);
      temp.random = this.recursive(node.random, map);
      return temp;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/544972809/){:target="_blank"}

# 설명
1. 주어진 임의 포인터와 다음 Node를 이어주는 연결된 Node인 head를 이용하여 동일한 형태로 새롭게 구성된 연결된 Node를 만드는 문제이다.
- 임의 포인터와 Node들은 주어진 Node인 head와 연결된 모든 Node들과 연관되어서는 안된다.

2. 재귀 호출을 이용하여 주어진 Node인 head를 Map을 새로 정의하여 동일한 형태로 새롭게 구성된 연결된 Node를 만들어 주어진 문제의 결과로 반환한다.
- head가 null인 경우 해당 Node가 존재하지 않는다는 의미이므로, null을 반환한다.
- map에 node가 존재하는 경우 이전에 해당 값에 해당하는 Node를 만나서 새로운 Node로 만들어 map에 저장된 경우이므로, map에서 node를 꺼내 반환한다.
- 그 외의 경우 새로운 Node를 만들어야 하므로, node를 이용하여 새로운 Node인 temp를 만들어 map에 넣어주고 temp.next와 temp.random의 Node는 재귀 호출을 이용하여 Node를 연결시켜주고 temp를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CopyListWithRandomPointer.java){:target="_blank"}에서 확인 가능합니다.