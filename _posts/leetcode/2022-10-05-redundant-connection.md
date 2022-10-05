---
title: "Leetcode Java Redundant Connection"
excerpt: "Leetcode Redundant Connection Java"
last_modified_at: 2022-10-05T21:20:00
header:
  image: /assets/images/leetcode/redundant-connection.png
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
[Link](https://leetcode.com/problems/redundant-connection){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findRedundantConnection(int[][] edges) {
    int[] parents = new int[edges.length + 1];
    for (int[] edge : edges) {
      int a = this.find(parents, edge[0]);
      int b = this.find(parents, edge[1]);
      if (a == b) {
        return edge;
      } else {
        parents[a] = b;
      }
    }
    return new int[] {};
  }

  private int find(int[] parents, int index) {
    return parents[index] == 0 ? index : this.find(parents, parents[index]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/815723816/){:target="_blank"}

# 설명
1. 트리 형태로 구성된 edges가 주어지면 n개의 노드로 구성된 트리가 되도록 제거할 배열을 찾는 문제이다.
- edges[i] = [a<sub>i</sub>, b<sub>i</sub>] 는 그래프에서 노드 a<sub>i</sub>와 b<sub>i</sub> 사이에 edge가 있음을 나타낸다.
- 제거할 edges 내 배열이 여러 개일 경우, 마지막 하나를 반환한다.

2. parents는 edges내 값들을 저장할 배열로, 최댓값으로 가능한 $edges.length + 1$ 크기의 정수 배열로 초기화한다.

3. edges의 모든 배열들을 순차적으로 각자 edge로 정의하여 아래를 반복한다.
- a에 4번에서 정의한 find(int[] parents, int index) 메서드를 이용하여 parents 배열에서 edge[0] 값에 해당하는 부모 노드의 값을 넣어준다.
- a에 4번에서 정의한 find(int[] parents, int index) 메서드를 이용하여 parents 배열에서 edge[1] 값에 해당하는 부모 노드의 값을 넣어준다.
- a와 b가 동일한 경우 동일한 부모 노드를 가지고 있으므로 제거해야 할 edge이므로, edge를 주어진 문제의 결과로 반환한다.
- a와 b가 동일하지 않은 경우, parents의 a번째 위치에 b를 넣어 부모 노드의 값을 저장하고 반복을 계속 수행한다.

4. 부모 노드의 값을 탐색하기 위한 find(int[] parents, int index) 메서드를 정의한다.
- parents의 index번째 값이 0이면 부모가 존재하지 않으므로, index를 반환한다.
- 위의 경우가 아니라면 index의 부모 노드 값으로 재귀 호출하여 더 상위 부모 노드의 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RedundantConnection.java){:target="_blank"}에서 확인 가능합니다.