---
title: "Leetcode Java Robot Bounded In Circle"
excerpt: "Leetcode Robot Bounded In Circle Java"
last_modified_at: 2024-03-11T18:20:00
header:
  image: /assets/images/leetcode/robot-bounded-in-circle.png
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
[Link](https://leetcode.com/problems/robot-bounded-in-circle){:target="_blank"}

# 코드
```java
class Solution {

  private static final int[][] DIRECTIONS = {
    { 0, 1 },
    { -1, 0 },
    { 0, -1 },
    { 1, 0 }
  };

  public boolean isRobotBounded(String instructions) {
    int i = 0;
    int[] point = new int[2];
    for (char c : instructions.toCharArray()) {
      switch (c) {
        case 'L': i = (i + 1) % 4; break;
        case 'R': i = (i + 3) % 4; break;
        default:
          point[0] += DIRECTIONS[i][0];
          point[1] += DIRECTIONS[i][1];
      }
    }
    return point[0] == 0 && point[1] == 0 || i != 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/robot-bounded-in-circle/submissions/1200380179/){:target="_blank"}

# 설명
1. 로봇이 [0, 0] 위치에서 위로 움직여 instructions의 처음부터 끝까지 문자들을 아래의 규칙대로 계속 수행할 때 시작 위치를 기준으로 계속 재귀하는지 검증하는 문제이다.
- 'G'는 1칸 직진한다.
- 'L'은 좌측(시계 반대 방향)으로 이동한다.
- 'R'은 우측(시계 방향)으로 이동한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- DIRECTIONS는 방향을 저장할 전역 변수로, 위 - 왼쪽 - 아래 - 오른쪽 방향으로 이동하기 위한 가감치를 넣어 정의한다.
- i는 이동 방향을 DIRECTIONS에 존재하는 값의 위치 값을 저장할 변수로, 초기 방향인 0으로 초기화한다.
- point는 현재 위치의 좌표를 저장할 변수로, 2차원 정수 배열로 초기화한다.

3. instructions의 각 문자를 c에 넣어 순차적으로 아래를 수행한다.
- c가 'L'인 경우, $i + 1$의 값을 4로 나눈 나머지 값을 넣어준다.
- c가 'R'인 경우, $i + 3$의 값을 4로 나눈 나머지 값을 넣어준다.
- 그 외의 c가 'G'인 경우, point의 각 자리에 DIRECTIONS[i]의 값을 더해준다.

4. 반복이 완료되면 아래의 조건 중 하나라도 만족하면 true를 아니면 false를 주어진 문제의 결과로 반환한다.
- point가 [0, 0]의 위치로 돌아오는 경우.
- i가 0이 아닌 초기 방향과 달라서, 앞의 순서대로 다시 반복하면 원래 자리로 돌아오는 경우.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RobotBoundedInCircle.java){:target="_blank"}에서 확인 가능합니다.