---
title: "Leetcode Java Count the Number of Complete Components"
excerpt: "Leetcode - 'Count the Number of Complete Components' 문제 Java 풀이"
last_modified_at: 2025-03-22T13:30:00
header:
  image: /assets/images/leetcode/count-the-number-of-complete-components.png
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
[Link](https://leetcode.com/problems/count-the-number-of-complete-components/){:target="_blank"}

# 코드
```java
class Solution {

  public int countCompleteComponents(int n, int[][] edges) {
    List<Integer>[] graph = new ArrayList[n];
    for (int i = 0; i < n; i++) {
      graph[i] = new ArrayList<>();
    }
    for (int[] edge : edges) {
      graph[edge[0]].add(edge[1]);
      graph[edge[1]].add(edge[0]);
    }
    boolean[] visited = new boolean[n];
    int result = 0;
    for (int i = 0; i < n; i++) {
      if (!visited[i]) {
        Set<Integer> set = new HashSet<>();
        int count = this.dfs(graph, visited, set, i);
        if (set.size() == 1 && set.contains(count - 1)) {
          result++;
        }
      }
    }
    return result;
  }

  private int dfs(List<Integer>[] graph, boolean[] visited, Set<Integer> set, int index) {
    visited[index] = true;
    set.add(graph[index].size());
    int count = 1;
    for (int neighbor : graph[index]) {
      if (!visited[neighbor]) {
        count += this.dfs(graph, visited, set, neighbor);
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-the-number-of-complete-components/submissions/1581913830/){:target="_blank"}

# 설명
1. n 개의 컴포넌트와 연결선 정보인 edges를 이용하여 컴포넌트의 각 요소끼리 모두 연결된 완전한 컴포넌트 그룹의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- graph는 각 연결 요소의 정보들을 각각 저장할 배열로, 각 위치 값을 ArrayList로 초기화하고 edges를 반복하여 각 컴포넌트 숫자 위치에 상대 컴포넌트 숫자를 저장해준다.
- visited는 컴포넌트의 방문 여부를 저장하기 위한 변수로, n 크기의 부울 배열로 초기화한다.
- result는 완벽한 컴포넌트 그룹의 수를 저장할 변수로, 0으로 초기화한다.

3. DFS 방식으로 컴포넌트를 탐색할 dfs(List<Integer>[] graph, boolean[] visited, Set<Integer> set, int index) 메서드를 정의한다.
- visited[index]의 값을 true로 바꾸어 방문한 위치인 것을 표시한다.
- count는 컴포넌트의 수를 계산할 변수로, 현재 컴포넌트를 포함하여 1로 초기화한다.
- graph[index]에 해당하는 인접한 컴포넌트 값을 neighbor에 순차적으로 넣어 아래를 반복하여 index에 해당 값을 넣어 재귀 호출하여 count를 증가시켜준다.
- 계산된 count를 반환한다.

4. 0부터 n 미만까지 i를 증가시키며 아래를 반복한다.
- visited[i]의 값이 false인 방문하지 않은 경우, 아래를 수행한다.
  - set은 각 컴포넌트와 연결된 컴포넌트 갯수를 저장할 변수로, 중복을 배제하기 위해 set으로 초기화한다.
  - count에는 3번에서 정의한 dfs(List<Integer>[] graph, boolean[] visited, Set<Integer> set, int index)를 수행한 결과를 저장한다.
  - set의 값이 하나인 각 컴포넌트에서 연결되지 않은 특정 컴포넌트가 포함되어 있지 않으면서, 컴포넌트 갯수인 $count - 1$이 존재하면 조건에 충족하므로 result를 증가시켜준다.

5. 반복이 완료되면 완전한 컴포넌트 그룹의 갯수가 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountTheNumberOfCompleteComponents.java){:target="_blank"}에서 확인 가능합니다.