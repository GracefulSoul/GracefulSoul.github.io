---
title: "Leetcode Java Keys and Rooms"
excerpt: "Leetcode Keys and Rooms Java"
last_modified_at: 2023-02-16T19:20:00
header:
  image: /assets/images/leetcode/keys-and-rooms.png
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
[Link](https://leetcode.com/problems/keys-and-rooms){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canVisitAllRooms(List<List<Integer>> rooms) {
    boolean[] visited = new boolean[rooms.size()];
    List<Integer> firstRoom = rooms.get(0);
    for (int i = 0; i < firstRoom.size(); i++) {
      this.dfs(rooms, visited, firstRoom.get(i));
    }
    for (int i = 1; i < visited.length; i++) {
      if (!visited[i]) {
        return false;
      }
    }
    return true;
  }

  private void dfs(List<List<Integer>> rooms, boolean[] visited, int index) {
    visited[index] = true;
    List<Integer> room = rooms.get(index);
    for (int i = 0; i < room.size(); i++) {
      if (!visited[room.get(i)]) {
        this.dfs(rooms, visited, room.get(i));
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/keys-and-rooms/submissions/899064136/){:target="_blank"}

# 설명
1. rooms의 첫 방을 제외한 나머지 방들이 잠길 때, 방 안에 열 수 있는 방의 키를 사용하여 모든 룸을 방문할 수 있는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- visited는 방의 방문 여부를 검증하기 위한 변수로, rooms의 방의 개수만큼의 크기로 초기화한다.
- firstRoom은 rooms 내 첫 방을 저장한 변수이다.

3. firstRoom의 모든 키를 이용하여 4번에서 정의한 dfs(List<List<Integer>> rooms, boolean[] visited, int index) 메서드의 index에 넣어 수행한다.

4. DFS 방식으로 모든 방을 검증하기 위한 dfs(List<List<Integer>> rooms, boolean[] visited, int index) 메서드를 정의한다.
- visited의 index번째 방을 방문했으므로, 해당 위치에 true를 넣어준다.
- room에 rooms의 index번째 방의 값을 넣어준다.
- room의 모든 키들을 이용하여 방문하지 않은 방인 경우, index에 room의 i번째 키를 이용하여 재귀 호출을 수행한다.

5. visited의 모든 값을 이용하여 방문하지 않은 방이 있으면 false를, 모두 방문했으면 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KeysAndRooms.java){:target="_blank"}에서 확인 가능합니다.