---
title: "Leetcode Java Shortest Distance After Road Addition Queries I"
excerpt: "Leetcode - 'Shortest Distance After Road Addition Queries I' 문제 Java 풀이"
last_modified_at: 2024-11-27T19:10:00
header:
  image: /assets/images/leetcode/shortest-distance-after-road-addition-queries-i.png
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
[Link](https://leetcode.com/problems/shortest-distance-after-road-addition-queries-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] shortestDistanceAfterQueries(int n, int[][] queries) {
    List<List<Integer>> list = new ArrayList<>();
    for (int i = 0; i < n; i++) {
      list.add(new ArrayList<>());
      list.get(i).add(i + 1);
    }
    int length = queries.length;
    int[] result = new int[length];
    for (int i = 0; i < length; i++) {
      int[] query = queries[i];
      list.get(query[0]).add(query[1]);
      result[i] = this.getShortestDistance(list, n);
    }
    return result;
  }

  private int getShortestDistance(List<List<Integer>> list, int n) {
    Queue<int[]> queue = new LinkedList<>();
    queue.offer(new int[] { 0, 0 });
    boolean[] visited = new boolean[n];
    visited[0] = true;
    while (!queue.isEmpty()) {
      int[] curr = queue.poll();
      if (curr[0] == n - 1) {
        return curr[1];
      }
      for (int neighbor : list.get(curr[0])) {
        if (!visited[neighbor]) {
          queue.offer(new int[] { neighbor, curr[1] + 1 });
          visited[neighbor] = true;
        }
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shortest-distance-after-road-addition-queries-i/submissions/1464127965/){:target="_blank"}

# 설명
1. 앞 도시와 뒤 도시가 연결된 n개의 도시와 신규 도로의 정보가 담긴 queries를 순서대로 완공할 때, 각 도로가 완성될 때마다 0번 도시에서 $n - 1$번 도시까지 도착하는 가장 짧은 거리를 각각 계산하여 배열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- list는 각 도시 별 연결된 도시를 저장할 변수로, ArrayList로 초기화하고 list의 각 도시에 해당하는 위치를 ArrayList를 넣어 다음 도시 번호를 초기값으로 넣어준다.
- length는 queries의 길이를 저장한 변수이다.
- result는 queries의 도로가 생성될 때 마다 최소 길이를 저장할 변수로, length 크기의 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- query에 queries[i]의 값을 넣어준다.
- list에서 query[0]의 값에 해당하는 위치에 query[1]의 값을 넣어준다.
- result[i]에 4번에서 정의한 getShortestDistance(List<List<Integer>> list, int n) 메서드를 수행한 결과를 넣어준다.

4. 0번 도시에서 $n - 1$번 도시까지 최단 경로를 구하기 위한 getShortestDistance(List<List<Integer>> list, int n) 메서드를 정의한다.
- queue는 도시의 각 경로를 넣어 최단 경로를 구하기 위한 변수로, LinkedList로 초기화하고 [0, 0]을 초기 값으로 넣어준다.
- visited는 도시 방문 여부를 저장할 변수로, 도시 갯수인 n 크기의 부울 배열로 초기화하고 처음 도시의 위치인 visited[0]을 true로 넣어준다.
- queue의 값이 비어있지 않을 때 까지 아래를 반복한다.
  - curr에 queue의 첫 값을 꺼내 넣어준다.
  - curr[0]의 값이 $n - 1$인 마지막 도시인 경우, curr[1]의 값인 현재까지 거리를 반환한다.
  - list의 curr[0]의 값을 순차적으로 neighbor에 넣고, visited[neighbor]의 값이 false인 방문하지 않은 경우만 queue에 neighbor의 값과 거리를 증가시킨 $curr[1] + 1$의 값을 배열로 넣고 visited[neighbor]의 값을 true로 초기화한다.
- 반복이 완료되면 마지막 도시까지 이동이 불가능하므로, -1을 반환한다.

5. 3번의 반복이 완료되면 각 도로가 완공될 때 마다 최단 거리가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestDistanceAfterRoadAdditionQueriesI.java){:target="_blank"}에서 확인 가능합니다.