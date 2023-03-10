---
title: "Leetcode Java Number of Provinces"
excerpt: "Leetcode Number of Provinces Java"
last_modified_at: 2022-06-27T19:00:00
header:
  image: /assets/images/leetcode/number-of-provinces.png
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
[Link](https://leetcode.com/problems/number-of-provinces/){:target="_blank"}

# 코드
```java
class Solution {

  public int findCircleNum(int[][] isConnected) {
    int length = isConnected.length;
    boolean[] visited = new boolean[length];
    int count = 0;
    for (int idx = 0; idx < length; idx++) {
      if (!visited[idx]) {
        this.dfs(isConnected, visited, idx);
        count++;
      }
    }
    return count;
  }

  private void dfs(int[][] isConnected, boolean[] visited, int i) {
    for (int j = 0; j < isConnected.length; j++) {
      if (isConnected[i][j] == 1 && !visited[j]) {
        visited[j] = true;
        this.dfs(isConnected, visited, j);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/732470404/){:target="_blank"}

# 설명
1. 각 도시의 연결 상태를 나타내는 isConnected를 이용하여 연결된 도시들은 하나의 지방으로 묶어주고, 지방의 수를 구하는 문제이다.
- isConnected[i][j] 의 값이 1인 경우, i번째 도시와 j번째 도시가 연결되어 하나의 지방으로 구성된다.
- isConnected[i][j] 의 값이 0인 경우, i번째 도시와 j번째 도시는 연결되지 않아 각 지방으로 분리된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 isConnected의 길이인 도시의 개수를 저장할 변수이다.
- visited는 방문 여부를 저장할 배열로, length 길이로 초기화한다.
- count는 지방의 개수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 length까지 idx를 증가시키며 아래를 수행한다.
- visited의 idx번째 값이 false인 방문하지 않은 경우, 4번에서 정의한 dfs(int[][] isConnected, boolean[] visited, int i) 메서드를 수행하고 count를 증가한다.

4. DFS 방식으로 visited에 값을 넣을 dfs(int[][] isConnected, boolean[] visited, int i) 메서드를 정의한다.
- 0부터 isConnected의 길이 미만까지 j를 증가시키며 isConnected[i][j]가 1로 연결되어있고 visited[j]가 false인 방문하지 않은 경우, visited의 j번째 값을 true로 바꾸고 i에 j를 넣어 재귀 호출을 수행한다.

5. 반복이 완료되면 지방의 개수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfProvinces.java){:target="_blank"}에서 확인 가능합니다.