---
title: "Leetcode Java Find Center of Star Graph"
excerpt: "Leetcode Find Center of Star Graph Java"
last_modified_at: 2024-06-27T19:50:00
header:
  image: /assets/images/leetcode/find-center-of-star-graph.png
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
[Link](https://leetcode.com/problems/find-center-of-star-graph/){:target="_blank"}

# 코드
```java
class Solution {

  public int findCenter(int[][] edges) {
    return edges[0][0] == edges[1][0] || edges[0][0] == edges[1][1] ? edges[0][0] : edges[0][1];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-center-of-star-graph/submissions/1301864472/){:target="_blank"}

# 설명
1. 별모양으로 연결된 노드들의 연결 선 정보가 담긴 edges를 이용하여 중앙에 있는 노드의 값을 반환하는 문제이다.

2. 중앙에 있는 노드의 값은 각 edge에 하나 씩 존재하므로, edges[0]과 edges[1]의 연결 선 정보를 이용하여 두 선에서 존재하는 노드 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindCenterOfStarGraph.java){:target="_blank"}에서 확인 가능합니다.