---
title: "Leetcode Java Find Champion II"
excerpt: "Leetcode - 'Find Champion II' 문제 Java 풀이"
last_modified_at: 2024-11-26T19:30:00
header:
  image: /assets/images/leetcode/find-champion-ii.png
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
[Link](https://leetcode.com/problems/find-champion-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int findChampion(int n, int[][] edges) {
    boolean[] weak = new boolean[n];
    for (int[] edge : edges) {
      weak[edge[1]] = true;
    }
    int result = -1;
    for (int i = 0; i < n; i++) {
      if (!weak[i]) {
        if (result == -1) {
          result = i;
        } else {
          return -1;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-champion-ii/submissions/1463239304/){:target="_blank"}

# 설명
1. n개의 팀이 있는 DAG(순환되지 않는 연결 선)이 저장된 edges를 이용하여 아래 규칙대로 토너먼트에서 우승할 팀을 구하는 문제이다.
- edges 내 임의 값인 edge = [i, j]로, i 팀이 j 팀보다 강한 것을 의미한다.
- 우승할 한 팀이 존재하지 않는 경우, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- weak는 약한 팀을 구분할 변수로, n 크기의 부울 배열로 초기화하고 edges의 각 두 번째 값들의 위치에 true를 넣어준다.
- result는 토너먼트 우승 팀을 저장할 변수로, 존재하지 않을 경우 반환할 값인 -1로 초기화한다.

3. 0부터 n 미만까지 i를 감소시키며 아래를 반복한다.
- weak[i]의 값이 false인 자신보다 강한 팀이 없는 경우, 아래를 수행한다.
  - result가 -1인 지금까지 우승할 팀이 존재하지 않으면, 현재 위치인 i를 넣어준다.
  - 위의 경우가 아니라면 강한 척도를 구분할 수 없는 팀이 둘 이상이므로, -1을 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 토너먼트 우승할 팀이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindChampionII.java){:target="_blank"}에서 확인 가능합니다.