---
title: "Leetcode Java Minimum Number of Vertices to Reach All Nodes"
excerpt: "Leetcode - 'Minimum Number of Vertices to Reach All Nodes' 문제 Java 풀이"
last_modified_at: 2023-05-18T19:05:00
header:
  image: /assets/images/leetcode/minimum-number-of-vertices-to-reach-all-nodes.png
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
[Link](https://leetcode.com/problems/minimum-number-of-vertices-to-reach-all-nodes){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> findSmallestSetOfVertices(int n, List<List<Integer>> edges) {
    boolean[] visited = new boolean[n];
    for (List<Integer> edge : edges) {
      visited[edge.get(1)] = true;
    }
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < n; i++) {
      if (!visited[i]) {
        result.add(i);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-vertices-to-reach-all-nodes/submissions/952635654/){:target="_blank"}

# 설명
1. n개의 꼭짓점이 존재하는 비순환 그래프인 edges를 이용하여 아래의 조건을 만족하면서 그래프의 모든 노드에 도달할 수 있는 가장 작은 수의 시작 노드를 찾는 문제이다.
- edges[i] = [from<sub>i</sub>, to<sub>i</sub>]로, from<sub>i</sub> 노드에서 to<sub>i</sub>로 이동할 수 있음을 나타낸다.

2. 문제 풀이에 필요한 변수를 정의한다.
- visited는 노드의 방문 여부를 저장하기 위한 변수로, n 크기의 부울 배열로 정의하고 edges를 이용하여 도착 노드의 번호에 true를 넣어준다.
- result는 시작 노드를 저장할 변수로, ArrayList로 초기화하고 0부터 n 미만까지 반복하여 도착 노드가 없는 노드들을 넣어준다.

3. 반복이 완료되면 가장 작은 수의 시작 노드들이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfVerticesToReachAllNodes.java){:target="_blank"}에서 확인 가능합니다.