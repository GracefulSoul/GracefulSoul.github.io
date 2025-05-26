---
title: "Leetcode Java Largest Color Value in a Directed Graph"
excerpt: "Leetcode - 'Largest Color Value in a Directed Graph' 문제 Java 풀이"
last_modified_at: 2025-05-26T19:40:00
header:
  image: /assets/images/leetcode/largest-color-value-in-a-directed-graph.png
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
[Link](https://leetcode.com/problems/largest-color-value-in-a-directed-graph/){:target="_blank"}

# 코드
```java
class Solution {

  public int largestPathValue(String colors, int[][] edges) {
    char[] charArray = colors.toCharArray();
    int length = charArray.length;
    List<Integer>[] graph = new List[length];
    for (int i = 0; i < length; i++) {
      graph[i] = new ArrayList<>();
    }
    int[] indegree = new int[length];
    for (int[] edge : edges) {
      indegree[edge[1]]++;
      graph[edge[0]].add(edge[1]);
    }
    int[][] counts = new int[length][26];
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < length; i++) {
      if (indegree[i] == 0) {
        queue.offer(i);
      }
    }
    int visited = 0;
    int result = 0;
    while (!queue.isEmpty()) {
      visited++;
      int curr = queue.poll();
      int color = charArray[curr] - 'a';
      result = Math.max(result, ++counts[curr][color]);
      for (int value : graph[curr]) {
        for (int i = 0; i < 26; i++) {
          counts[value][i] = Math.max(counts[value][i], counts[curr][i]);
        }
        if (--indegree[value] == 0) {
          queue.offer(value);
        }
      }
    }
    return visited == length ? result : -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-color-value-in-a-directed-graph/submissions/1644878492/){:target="_blank"}

# 설명
1. 각 노드의 색상을 'a' 부터 'z'까지로 정의한 colors와 노드 간 연결 정보가 저장된 edges를 이용하여 순환되지 않는 직렬로 연결된 선 중 가장 많은 색상의 수를 구하는 문제이다.
- 선이 순환되는 경우, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 colors를 문자 배열로 변환한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.
- graph는 노드 간 연결 정보를 저장할 변수로, length 크기의 List 배열로 초기화한다.
- indegree는 간선 정보를 저장할 변수로, length 길이의 정수 배열로 초기화한다.
  - edges를 순차적으로 edge에 넣어 indegree 내 연결된 edge[1] 번째 값을 증가시키고, graph의 edge[0] 노드 값의 위치에 edge[1] 노드 값을 넣어준다.
- counts는 색상의 갯수를 계산할 변수로, $length \times 26$ 크기의 2차원 정수 배열로 초기화한다.
- queue는 노드를 순차적으로 넣어 탐색하기 위한 변수로, LinkedList로 초기화 후 indegree 값 존재하는 위치 값을 넣어준다.
- visited는 탐색한 위치 값을 저장하기 위한 변수로, 0으로 초기화한다.
- result는 연결선 중 가장 많은 색상의 수를 저장하기 위한 변수로, 0으로 초기화한다.

3. queue가 비어있지 않을 때까지 아래를 반복한다.
- visited를 증가시켜 탐색한 위치를 기록한다.
- curr은 현재 노드 값을, color는 charArray 내 curr번째 문자의 영문자 순서를 저장한다.
- counts[curr][color]의 값을 증가시킨 후 result에 result와 해당 값 중 큰 값을 넣어준다.
- graph[curr]의 값을 순차적으로 value에 넣고 아래를 반복한다.
  - 0부터 26 미만까지 i를 증가시키며 counts[value][i]의 위치에 기존 값과 counts[curr][i]의 값인 현재 노드까지 포함된 갯수 중 큰 값을 반복하여 저장한다.
  - indegree[value]의 값을 감소시킨 후 값이 0인 연결된 간선 정보가 없는 경우, queue에 value를 넣어 앞의 노드 계산을 수행하도록 한다.

4. 반복이 완료되면 visited의 값이 length인 마지막까지 탐색한 경우, result를 아니면 -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestColorValueInADirectedGraph.java){:target="_blank"}에서 확인 가능합니다.