---
title: "Leetcode Java Walking Robot Simulation"
excerpt: "Leetcode Walking Robot Simulation Java"
last_modified_at: 2023-03-15T08:30:00
header:
  image: /assets/images/leetcode/walking-robot-simulation.png
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
[Link](https://leetcode.com/problems/walking-robot-simulation){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[][] DIRECTIONS = new int[][] {
    { 0, 1 },
    { 1, 0 },
    { 0, -1 },
    { -1, 0 }
  };

  public int robotSim(int[] commands, int[][] obstacles) {
    Set<Integer> set = new HashSet<>();
    for (int[] obstacle : obstacles) {
      set.add(obstacle[0] + obstacle[1] * 40000);
    }
    int[] coordinate = new int[] { 0, 0 };
    int direction = 0;
    int result = 0;
    for (int command : commands) {
      if (command == -1) {
        direction = (direction + 1) % 4;
      } else if (command == -2) {
        direction = (direction - 1 + 4) % 4;
      } else {
        while (command-- > 0) {
          if (!set.contains((coordinate[0] + DIRECTIONS[direction][0]) + (coordinate[1] + DIRECTIONS[direction][1]) * 40000)) {
            coordinate[0] += DIRECTIONS[direction][0];
            coordinate[1] += DIRECTIONS[direction][1];
            result = Math.max(result, coordinate[0] * coordinate[0] + coordinate[1] * coordinate[1]);
          } else {
            break;
          }
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/walking-robot-simulation/submissions/915311329/){:target="_blank"}

# 설명
1. [0, 0]에서 출발하여 아래의 세 명령이 존재하는 commands를 이용하여 얻을 수 있는 최대 [Euclidean distance](https://en.wikipedia.org/wiki/Euclidean_distance){:target="_blank"}를 반환하는 문제이다.
- -2는 90도로 좌회전한다.
- -1은 90도로 우회전한다.
- 1 ~ 9는 각 거리만큼 앞으로 이동한다.

2. DIRECTIONS는 이동 방향을 저장할 변수로, 위쪽 방향부터 시계 방향으로 이동 방향을 넣어준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- set은 obstacle의 장애물 위치를 넣을 변수로, obstacle의 y 위치 값에 값 범위 밖의 수인 40,000을 곱한 값과 y 위치 값을 더해서 넣어준다.
- coordinate는 현재 위치를 저장할 변수로, x와 y의 위치가 [0, 0]으로 시작하므로 해당 값으로 초기화한 정수 배열로 정의한다.
- direction은 방향을 저장할 변수로, 0으로 초기화한다.
- result는 최대 유클리안 거리를 계산하여 저장할 변수로, 0으로 초기화한다.

4. commands의 모든 값들을 순차적으로 command에 넣어 아래를 수행한다.
- command가 -1인 경우, direction에 자신의 값을 증가시키고 overflow를 방지하기 위하여 4로 나눈 나머지 값을 넣어준다.
- command가 -2인 경우, direction에 자신의 값을 감소시키고 4를 더한 후 overflow를 방지하기 위하여 4로 나눈 나머지 값을 넣어준다.
- 그 외의 값인 경우, command를 감소시키며 0 초과일 때 까지 아래를 반복한다.
  - 현재 위치에서 이동한 위치에 장애물이 존재하지 않는 경우, coordinate의 값에 이동하는 방향의 값을 더하고 result에 현재까지 최대 유클리안 거리를 저장한 result와 현재 위치에서의 유클리안 거리를 계산한 값 중 큰 값을 넣어준다.
  - 현재 위치에서 이동한 위치에 장애물이 존재하는 경우 더 이상 이동이 불가능하기 때문에 반복을 중단한다.

5. 수행이 완료되면 최대 유클리안 거리가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WalkingRobotSimulation.java){:target="_blank"}에서 확인 가능합니다.