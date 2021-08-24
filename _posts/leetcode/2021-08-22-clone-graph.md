---
title: "Leetcode Java Clone Graph"
excerpt: "Leetcode Clone Graph Java 풀이"
last_modified_at: 2021-08-22T13:00:00
header:
  image: /assets/images/leetcode/clone-graph.png
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
[Link](https://leetcode.com/problems/clone-graph/){:target="_blank"}

# 코드
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/
class Solution {

  public Node cloneGraph(Node node) {
    Map<Integer, Node> map = new HashMap<Integer, Node>();
    return this.recursive(node, map);
  }

  private Node recursive(Node node, Map<Integer, Node> map) {
    if (node == null) {
      return null;
    } else if (map.containsKey(node.val)) {
      return map.get(node.val);
    } else {
      Node temp = new Node(node.val);
      map.put(temp.val, temp);
      for (Node neighbor : node.neighbors) {
        temp.neighbors.add(this.recursive(neighbor, map));
      }
      return temp;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/542213283/){:target="_blank"}

# 설명
1. 주어진 Node인 node를 이용하여 동일한 Node를 만드는 문제이다.

2. Node를 node.val 기준으로 임시 저장하기 위한 Map을 정의한다.

3. 재귀 호출을 수행하여 동일한 Node를 만들어 주어진 문제의 결과로 반환한다.
- node가 null인 경우 주어진 Node가 null인 경우이므로, 그대로 null을 반환한다.
- map에 node.val가 존재하는 경우 기존에 만들었던 Node가 존재한다는 의미이므로, map에서 해당 Node를 꺼내서 반환한다.
- 그 외의 경우 map에 존재하지 않는 Node이므로, node.val 값을 이용하여 새 Node를 만든 후 map에 임시 저장하고 재귀 호출을 이용하여 Neighbors를 찾아 추가하고 새 노드인 temp를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CloneGraph.java){:target="_blank"}에서 확인 가능합니다.