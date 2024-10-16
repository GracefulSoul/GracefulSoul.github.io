---
title: "Leetcode Java Unique Paths"
excerpt: "Leetcode Unique Paths Java 풀이"
last_modified_at: 2021-06-12T11:10:00
header:
  image: /assets/images/leetcode/unique-paths.png
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
[Link](https://leetcode.com/problems/unique-paths/){:target="_blank"}

# 코드
```java
class Solution {

  public int uniquePaths(int m, int n) {
    return this.recursiveUniquePaths(m - 1, n - 1, new int[n][m]);
  }

  private int recursiveUniquePaths(int m, int n, int[][] path) {
    if (m == 0 || n == 0) {
      return 1;
    } else if (path[n][m] > 0) {
      return path[n][m];
    } else {
      return path[n][m] = this.recursiveUniquePaths(m - 1, n, path) + this.recursiveUniquePaths(m, n - 1, path);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/506597064/){:target="_blank"}

# 설명
1. 주어진 정수 m는 2차원 배열의 세로, n은 가로 축으로 맨 처음 열과 행에서 출발하여 맨 마지막 열과 행에 도달하기 까지의 경우의 수를 구하는 문제이다.

2. 재귀 호출을 호출할 때 각 위치에 도달하기 까지의 경우의 수를 저장하는 배열 path를 선언하여, 해당 위치의 경우의 수를 저장하고 다른 위치에서의 경우의 수를 측정할 때 활용한다.

3. 재귀 호출을 통해 최종 위치의 값이 지정되면 해당 위치의 값을 주어진 문제의 결과로 반환한다.
- m이 0이거나 n이 0인 경우, 1을 반환하여 경우의 수를 추가한다.
- path[n][m]이 0보다 큰 경우, 해당 위치의 경우의 수가 존재하기 때문에 해당 값을 그대로 반환한다.
- 그 외의 경우 path[n, $m - 1$] 위치의 경우의 수와 path[$n - 1$, m]의 위치의 경우의 수를 재귀호출로 가져와 합쳐 path[n][m] 위치의 경우의 수로 넣는다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniquePaths.java){:target="_blank"}에서 확인 가능합니다.