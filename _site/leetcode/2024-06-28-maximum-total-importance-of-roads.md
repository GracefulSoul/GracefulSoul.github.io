---
title: "Leetcode Java Maximum Total Importance of Roads"
excerpt: "Leetcode Maximum Total Importance of Roads Java"
last_modified_at: 2024-06-28T20:00:00
header:
  image: /assets/images/leetcode/maximum-total-importance-of-roads.png
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
[Link](https://leetcode.com/problems/maximum-total-importance-of-roads/){:target="_blank"}

# 코드
```java
class Solution {

  public long maximumImportance(int n, int[][] roads) {
    long result = 0;
    long cost = 1;
    long[] connections = new long[n];
    for (int[] road : roads) {
      connections[road[0]]++;
      connections[road[1]]++;
    }
    Arrays.sort(connections);
    for (long connection : connections) {
      result += connection * (cost++);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-total-importance-of-roads/submissions/1303004475/){:target="_blank"}

# 설명
1. [0, $n - 1$] 범위 내 노드들과 각 노드간 연결 선이 저장된 roads를 이용하여 이용하여 [1, n] 범위의 값들을 각 노드의 이동 간 최대 점수가 될 수 있도록노드에 할당할 때, 최대 점수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최대 점수를 구하기 위한 변수로, 0으로 초기화한다.
- cost는 각 노드의 점수를 할당하기 위한 변수로, 최소 점수인 1로 초기화한다.
- connections는 각 노드간 연결 횟수를 저장할 변수로, n 크기의 long 배열로 초기화하여 roads의 시작점과 종료점의 갯수를 각각 넣어준 후 오름차순 정렬해준다.

3. connections의 각 값을 connection에 순차적으로 넣어 아래를 수행한다.
- result에 $connection \times cost$ 값을 넣고 cost를 증가시켜준다.

4. 반복을 통해 계산된 최대 점수인 result를 주어진 문제의 결과로 반환한다.

# 해설
- 연결 선의 수가 적은 노드인 경우, 이동 경로에 접점이 많이 발생하지 않으므로 점수를 순차적으로 연결 선의 수의 오름차순으로 할당한다.
- 위를 통하여 접점이 많은 노드는 최대 점수가 되어 각 이동 경로에 대한 점수 계산 시, 가장 많은 점수를 획득할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumTotalImportanceOfRoads.java){:target="_blank"}에서 확인 가능합니다.