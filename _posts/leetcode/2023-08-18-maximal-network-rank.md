---
title: "Leetcode Java Maximal Network Rank"
excerpt: "Leetcode Medium - 'Maximal Network Rank' 문제 Java 풀이"
last_modified_at: 2023-08-18T20:50:00
header:
  image: /assets/images/leetcode/maximal-network-rank.png
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
[Link](https://leetcode.com/problems/maximal-network-rank){:target="_blank"}

# 코드
```java
class Solution {

  public int maximalNetworkRank(int n, int[][] roads) {
    boolean[][] connect = new boolean[n][n];
    int[] count = new int[n];
    for (int[] road : roads) {
      count[road[0]]++;
      count[road[1]]++;
      connect[road[0]][road[1]] = true;
      connect[road[1]][road[0]] = true;
    }
    int result = 0;
    for (int i = 0; i < n; i++) {
      for (int j = i + 1; j < n; j++) {
        result = Math.max(result, count[i] + count[j] - (connect[i][j] ? 1 : 0));
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximal-network-rank/submissions/1024800457/){:target="_blank"}

# 설명
1. n개의 도시에 도시 간 이어주는 roads를 이용하여 가장 많은 도로가 이어진 도로의 수를 찾는 문제이다.
- 단, a와 b 두 도시가 이어있을 때 b에 연결된 도시들은 a와 연결되어 있는 것으로 취급한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- connect는 도시 간 이어진 정보를 저장하기 위한 변수로, $n \times n$ 크기의 2차원 부울 배열로 초기화한다.
- count는 도시 간 직접 이어진 도로의 수를 저장하기 위한 변수로, n 크기의 정수로 초기화한다.
  - roads의 모든 값을 이용하여 count와 connect를 초기화한다.
- result는 최대 연결된 도시의 수를 저장하기 위한 변수로, 0으로 초기화한다.

3. 0부터 n 미만까지 i를 증가시키고, $i + 1$부터 n 미만까지 j를 증가시키며 아래를 반복한다.
- result에 result와 count 내 i와 j번째 값의 합에 i와 j의 연결 되었으면 1을 더한 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 최대 연결된 도로의 수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximalNetworkRank.java){:target="_blank"}에서 확인 가능합니다.