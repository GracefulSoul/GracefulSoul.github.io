---
title: "Leetcode Java Minimum Height Trees"
excerpt: "Leetcode Minimum Height Trees Java 풀이"
last_modified_at: 2021-12-21T18:00:00
header:
  image: /assets/images/leetcode/minimum-height-trees.png
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
[Link](https://leetcode.com/problems/minimum-height-trees/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> findMinHeightTrees(int n, int[][] edges) {
    List<Integer> result = new ArrayList<>();
    if (n == 1) {
      result.add(0);
      return result;
    } else if (n == 2) {
      result.add(0);
      result.add(1);
      return result;
    }
    List<Integer>[] graph = new ArrayList[n];
    int[] degree = new int[n];
    for (int idx = 0; idx < n; idx++) {
      graph[idx] = new ArrayList<>();
    }
    for (int[] edge : edges) {
      int v1 = edge[0];
      int v2 = edge[1];
      degree[v1]++;
      degree[v2]++;
      graph[v1].add(v2);
      graph[v2].add(v1);
    }
    Deque<Integer> deque = new ArrayDeque<>();
    for (int idx = 0; idx < n; idx++) {
      if (degree[idx] == 1) {
        deque.add(idx);
      }
    }
    while (n > 2) {
      int size = deque.size();
      n -= size;
      while (size > 0) {
        int idx = deque.pop();
        degree[idx]--;
        for (int val : graph[idx]) {
          degree[val]--;
          if (degree[val] == 1) {
            deque.add(val);
          }
        }
        size--;
      }
    }
    result.addAll(deque);
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/604893522/){:target="_blank"}

# 설명
1. 주어진 정수 n과 정수 배열 edges를 이용하여 만든 Tree가 최소 높이가 되는 Tree들(Minimum Height Trees - MHTs)의 root의 값을 반환하는 문제이다.
- 주어진 정수 n은 Tree의 노드의 개수이자 노드의 값의 상한선($n - 1$)을 의미한다.
- 주어진 정수 배열인 edges는 노드간 연결 정보를 저장한 배열이다.

2. 최소 높이를 저장할 result인 List를 정의하여, 주어진 n이 1과 2인 경우 아래를 수행한다.
- 주어진 n이 1인 경우, result에 0을 넣어 주어진 문제의 결과로 반환한다.
- 주어진 n이 2인 경우, result에 0과 1을 넣어 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- graph는 가능한 Tree를 만들어 넣을 List의 배열로, n의 크기와 각 위치에 ArrayList를 초기화하여 넣어준다.
- degree는 각 graph의 각 높이를 저장할 배열로, n의 크기로 초기화한다.

4. edges를 반복하여 degree와 graph를 초기화한다.
- 지역 변수 v1에 edge[0], v2에 edge[1]을 넣어준다.
- degree의 v1번째 값과 v2번째 값을 증가시킨다.
- graph의 v1번째 List에 v2를 넣어주고, v2번째 List에 v1을 넣어준다.

5. deque를 정의하여 degree가 1인 값만 deque에 넣어준다.

6. n이 2보다 클 때까지 반복하여 deque에 최소 높이가 되는 Tree들(MHTs)의 root 값을 넣어준다.
- 지역 변수 size에 deque의 크기를 넣어준다.
- n에 해당 size 값을 빼준다.
- size가 0보다 클 때까지 다시 반복을 수행한다.
  - deque에서 값을 하나 꺼내와서 idx에 넣어준다.
  - graph의 idx번째 값들을 반복하여 degree의 해당 값의 위치 값을 빼주고, 해당 값이 1이 되면 deque에 넣어준다.
  - size를 감소시키고 반복을 계속 수행한다.

7. 반복이 완료되면 최소 높이가 되는 Tree들(MHTs)의 root 값들을 넣은 deque의 모든 값들을 result에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumHeightTrees.java){:target="_blank"}에서 확인 가능합니다.