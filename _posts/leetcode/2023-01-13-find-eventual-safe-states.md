---
title: "Leetcode Java Find Eventual Safe States"
excerpt: "Leetcode Find Eventual Safe States Java"
last_modified_at: 2023-01-13T19:30:00
header:
  image: /assets/images/leetcode/find-eventual-safe-states.png
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
[Link](https://leetcode.com/problems/find-eventual-safe-states){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> eventualSafeNodes(int[][] graph) {
    List<Integer> result = new ArrayList<>();
    int length = graph.length;
    int[] state = new int[length];
    for (int idx = 0; idx < length; idx++) {
      if (this.dfs(graph, state, idx)) {
        result.add(idx);
      }
    }
    return result;
  }

  private boolean dfs(int[][] graph, int[] state, int index) {
    if (state[index] != 0) {
      return state[index] == 1;
    } else {
      state[index] = 2;
      for (int node : graph[index]) {
        if (!this.dfs(graph, state, node)) {
          return false;
        }
      }
      state[index] = 1;
      return true;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-eventual-safe-states/submissions/877369039/){:target="_blank"}

# 설명
1. [0, $n - 1$]까지 n개의 노드의 방향이 저장된 graph는 각각 아래의 노드로 구분이 되며, 그 중 안전한 노드를 찾아 오름차순으로 정렬하여 반환하는 문제이다.
- 터미널 노드는 나가는 방향이 없는 노드이다.
- 안전한 노드는 터미널 노드 또는 안전한 노드로 이어지는 노드이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 안전한 노드를 오름차순 저장하여 반환할 변수로, ArrayList로 초기화한다.
- length는 graph의 길이를 저장한 변수이다.
- state는 n개의 노드의 각 상태를 저장할 배열로, length 크기로 초기화하며 아래의 각 상태를 가진다.
  - 0은 아직 노드를 탐색하지 않은 값이다.
  - 1은 안전한 노드를 의미하는 값이다.
  - 2는 안전하지 않은 노드를 의미하는 값이다.

3. 0부터 length 미만까지 idx를 증가시키며 아래를 검증한다.
- 4번에서 정의한 dfs(int[][] graph, int[] state, int index) 메서드에 각 변수와 idx를 넣어 수행한 결과가 true인 안전한 노드인 경우, result에 idx를 넣어준다.

4. DFS 방식으로 graph 내 안전한 노드를 찾기 위한 dfs(int[][] graph, int[] state, int index) 메서드를 정의한다.
- state의 index번째 상태가 0인 탐색하지 않은 노드가 아니라면, 해당 값이 1인 안전한 노드인지 검증한 결과를 반환한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - state의 index번째 값에 안전하지 않은 노드라는 의미의 2를 넣어준다.
  - graph의 index번째 값들을 node에 넣어 반복하여 index 자리에 해당 값으로 재귀 호추한 결과가 false인 경우 안전하지 않은 노드이므로, false를 반환한다.
  - 위의 반복이 완료되면 안전한 노드이므로 state의 index번째 값에 1을 넣고, true를 반환한다.

5. 3번의 반복이 완료되면 안전한 노드를 오름차순으로 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindEventualSafeStates.java){:target="_blank"}에서 확인 가능합니다.