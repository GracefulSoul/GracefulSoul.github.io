---
title: "Leetcode Java Maximize the Number of Target Nodes After Connecting Trees I"
excerpt: "Leetcode - 'Maximize the Number of Target Nodes After Connecting Trees I' 문제 Java 풀이"
last_modified_at: 2025-05-28T22:10:00
header:
  image: /assets/images/leetcode/maximize-the-number-of-target-nodes-after-connecting-trees-i.png
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
[Link](https://leetcode.com/problems/maximize-the-number-of-target-nodes-after-connecting-trees-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] maxTargetNodes(int[][] edges1, int[][] edges2, int k) {
    List<List<Integer>> list = this.parseList(edges2);
    int max = 0;
    for (int i = 0; i < list.size(); i++) {
      max = Math.max(max, this.dfs(list, k - 1, i, -1));
    }
    list = this.parseList(edges1);
    int length = list.size();
    int[] result = new int[length];
    for (int i = 0; i < length; i++) {
      result[i] = this.dfs(list, k, i, -1) + max;
    }
    return result;
  }

  private List<List<Integer>> parseList(int[][] edges) {
    int length = edges.length + 1;
    List<List<Integer>> list = new ArrayList<>(length);
    for (int i = 0; i < length; i++) {
      list.add(new ArrayList<>());
    }
    for (int[] edge : edges) {
      list.get(edge[0]).add(edge[1]);
      list.get(edge[1]).add(edge[0]);
    }
    return list;
  }

  private int dfs(List<List<Integer>> list, int k, int i, int target) {
    if (k < 0) {
      return 0;
    } else {
      int count = 1;
      for (int value : list.get(i)) {
        if (value != target) {
          count += this.dfs(list, k - 1, value, i);
        }
      }
      return count;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximize-the-number-of-target-nodes-after-connecting-trees-i/submissions/1646918953/){:target="_blank"}

# 설명
1. 노드간 연결 선 정보가 있는 edges1, edges2를 이용하여 edges1에서 edges2의 임의 노드에 연결하여 k번 이하 이동을 통해 연결할 수 있는 최대 노드의 갯수를 반환하는 문제이다.

2. 각 edges 배열을 이용하여 노드 연결 정보를 List로 변환할 parseList(int[][] edges) 메서드를 정의한다.
- length는 list의 길이를 저장할 변수로, [0, $n - 1$] 범위의 값이 존재하므로 edges의 길이보다 1 큰 값을 넣어준다.
- list는 각 노드의 연결 정보를 저장할 변수로, [0, $n - 1$] 위치에 ArrayList를 넣어 초기화 후 edges를 순차적으로 edge에 넣고 각 노드 위치에 반대편 노드 위치를 넣어주 후 반환한다.

3. DFS 방식으로 연결된 노드의 갯수를 계산할 dfs(List\<List\<Integer\>\> list, int k, int i, int target) 메서드를 정의한다.
- k가 0 미만인 이동 위치가 없으면, 0을 반환한다.
- k가 0 이상인 경우, 아래를 반복한다.
  - count는 연결된 노드 갯수를 계산하기 위한 변수로, 현재 연결된 노드를 포함하여 1로 초기화한다.
  - list의 i번째 값들을 순차적으로 value에 넣고 k에 $k - 1$인 이동 횟수를 차감 후 i와 target 위치에 value와 i를 순차적으로 넣어 재귀 호출한 값을 count에 더해준다.
  - 반복을 통해 계산된 count를 반환한다.

4. 문제 풀이에 필요한 변수를 정의한다.
- list는 연결된 노드 정보를 저장할 변수로, 우선 edges2로 parseList(int[][] edges) 메서드를 수행한 결과를 넣어준다.
- max는 edges2에서 k 이동거리 내 노드가 최대인 갯수를 저장할 변수로, list를 반복하여 k에 $k - 1$인 이동 횟수를 차감 후 target 위치에 -1을 넣어 dfs(List\<List\<Integer\>\> list, int k, int i, int target) 메서드를 수행한 값 중 최댓값을 저장한다.
- length는 edges1의 길이를 저장한 변수이다.
- result는 결과를 저장할 변수로, length 길이의 정수 배열로 초기화한다.

5. list에 다시 edges1으로 parseList(int[][] edges) 메서드를 수행한 결과를 넣어준다.

6. 0부터 length 미만까지 i를 증가시키며, result[i]의 위치에 아래 두 값의 합을 넣어준다.
- target을 -1로 넣고 dfs(List\<List\<Integer\>\> list, int k, int i, int target) 메서드를 수행한 결과인 edges1 내 i번째 노드에서 연결 가능한 노드의 갯수.
- edges2에서 최대 연결 가능한 노드 갯수인 max의 값.

7. 반복이 완료되면 각 노드 별 최대 연결 가능한 노드의 수가 저장된 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximizeTheNumberOfTargetNodesAfterConnectingTreesI.java){:target="_blank"}에서 확인 가능합니다.