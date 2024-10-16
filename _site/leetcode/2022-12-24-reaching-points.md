---
title: "Leetcode Java Reaching Points"
excerpt: "Leetcode Reaching Points Java"
last_modified_at: 2022-12-24T10:30:00
header:
  image: /assets/images/leetcode/reaching-points.png
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
[Link](https://leetcode.com/problems/reaching-points){:target="_blank"}

# 코드
```java
class Solution {

  public boolean reachingPoints(int sx, int sy, int tx, int ty) {
    while (sx < tx && sy < ty) {
      if (tx < ty) {
        ty %= tx;
      } else {
        tx %= ty;
      }
    }
    return (sx == tx && sy <= ty && (ty - sy) % sx == 0) || (sy == ty && sx <= tx && (tx - sx) % sy == 0);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reaching-points/submissions/864506759/){:target="_blank"}

# 설명
1. [sx, sy] 위치에서 아래의 규칙대로 이동하여 [tx, ty]로 도착 가능한지 검증하는 문제이다.
- 시작 위치에서 (x, $x + y$) 혹은 ($x + y$, y)의 크기대로 이동할 수 있다.

2. sx가 tx보다 크고 sy가 ty보다 클 때 까지 아래를 수행한다.
- tx보다 ty가 큰 경우, ty에 tx를 나눈 나머지 값을 넣어준다.
- 위의 경우가 아니라면, tx에 ty를 나눈 나머지 값을 넣어준다.

3. 반복이 완료되면 아래의 경우를 검증하여 하나라도 만족하면 true를, 아니면 false를 주어진 문제의 결과로 반환한다.
- sx와 tx가 동일하면서 sy가 ty보다 작거나 같은 경우, ty에 sy를 빼서 sx를 나눈 나머지가 0인 경우.
- sy가 ty와 동일하면서 sx가 tx보다 작거나 같은 경우, tx에 sx를 빼서 sy를 나눈 나머지가 0인 경우.

# 해설
- 시작 위치에서 도착 위치를 탐색하기 가장 수월한 방법은 도착 위치에서 시작 위치로 회귀 가능한지 검증하는 것이다.
- 그렇기 때문에 ty와 tx를 위의 규칙에 대입해 여러 번 빼서 TLE(Time Limit Exceeded)가 발생하지 않도록 나머지 값을 활용해서 각 축의 위치를 좁혀간다.
- 결과에서 다시 규칙을 검증하는 이유는 2번의 수행이 완료되거나 수행하지 않는 한 축의 값이 동일한 경우, x축 혹은 y축의 값 중 최소 하나만 만족하는 경우로 끝나므로 각 축에 대해서 다시 이동 가능한지 마지막으로 검증하는 것이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReachingPoints.java){:target="_blank"}에서 확인 가능합니다.