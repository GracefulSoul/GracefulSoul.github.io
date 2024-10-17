---
title: "Leetcode Java K Closest Points to Origin"
excerpt: "Leetcode Medium - 'K Closest Points to Origin' 문제 Java 풀이"
last_modified_at: 2023-08-12T13:40:00
header:
  image: /assets/images/leetcode/k-closest-points-to-origin.png
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
[Link](https://leetcode.com/problems/k-closest-points-to-origin){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] kClosest(int[][] points, int k) {
    Queue<int[]> queue = new PriorityQueue<>((a, b) -> ((a[0] * a[0]) + (a[1] * a[1])) - ((b[0] * b[0]) + (b[1] * b[1])));
    int[][] result = new int[k][2];
    for (int[] point : points) {
      queue.add(point);
    }
    for (int i = 0; i < k; i++) {
      result[i] = queue.poll();
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/k-closest-points-to-origin/submissions/1018943255/){:target="_blank"}

# 설명
1. (0, 0) 좌표에서 가장 가까운 k개의 points를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- queue는 좌표의 거리를 저장할 변수로, PriorityQueue로 거리에 대한 오름차순으로 정렬하여 points의 모든 좌표값을 저장한다.
  - 길이의 비교는 제곱근을 수행하지 않아도 알 수 있으므로 제곱근을 수행하지 않은 값으로 비교한다.
- result는 k개의 좌표를 저장할 변수로, $k \times 2$ 크기의 배열로 초기화한다.

3. 0부터 k까지 queue의 좌표를 result에 넣어주고 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KClosestPointsToOrigin.java){:target="_blank"}에서 확인 가능합니다.