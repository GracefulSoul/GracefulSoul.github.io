---
title: "Leetcode Java Determine if a Cell Is Reachable at a Given Time"
excerpt: "Leetcode Determine if a Cell Is Reachable at a Given Time Java"
last_modified_at: 2023-11-08T18:50:00
header:
  image: /assets/images/leetcode/determine-if-a-cell-is-reachable-at-a-given-time.png
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
[Link](https://leetcode.com/problems/determine-if-a-cell-is-reachable-at-a-given-time){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isReachableAtTime(int sx, int sy, int fx, int fy, int t) {
    int x = Math.abs(sx - fx);
    int y = Math.abs(sy - fy);
    int min = Math.min(x, y) + Math.abs(y - x);
    if (min == 0) {
      return t != 1;
    } else {
      return t >= min;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/determine-if-a-cell-is-reachable-at-a-given-time/submissions/1094326636/){:target="_blank"}

# 설명
1. [sx, sy] 위치에서 [fx, fy] 위치까지 인접한 셀로 이동하는 시간일 1초일 때, t초 내 도달 가능한지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- x와 y는 x축과 y축의 차이를 넣을 변수로, $sx - fx$의 절댓값과 $sy - fy$의 절댓값으로 초기화한다.
- min은 최소 시간을 저장할 변수로, x와 y 중 작은 값에 $y - x$의 절댓값을 더해서 넣어준다.

4. min이 0인 경우, 시작과 종료가 동일한 위치인 경우이므로 t가 1이 아닌 경우만 주어진 문제의 결과로 true를 아니면 false로 반환한다.
  - t가 1인 경우, 어느 방향으로 이동하던지 자기 위치로 돌아올 수 없다.
  - t가 2인 경우, 어느 방향으로 이동했다 되돌아올 수 있다.
  - t가 3인 경우, 대각선을 활용하여 시작 위치에서 인접한 두 위치를 이동한 후 대각선으로 되돌아올 수 있다.
  - 위의 각 경우에서, 1인 경우는 복귀가 불가능하며 2 이상의 짝수는 왕래를 통해 가능하고, 3 이상의 홀수는 같은 프로세스로 가능하다.

5. min이 0이 아닌 경우에는, t가 min 이상인 최소 이동 거리에 속한다면 주어진 문제의 결과로 true로 아니면 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DetermineIfACellIsReachableAtAGivenTime.java){:target="_blank"}에서 확인 가능합니다.