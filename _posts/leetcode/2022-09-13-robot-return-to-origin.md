---
title: "Leetcode Java Robot Return to Origin"
excerpt: "Leetcode Robot Return to Origin Java"
last_modified_at: 2022-09-13T19:00:00
header:
  image: /assets/images/leetcode/robot-return-to-origin.png
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
[Link](https://leetcode.com/problems/robot-return-to-origin){:target="_blank"}

# 코드
```java

class Solution {

  public boolean judgeCircle(String moves) {
    int x = 0;
    int y = 0;
    for (char move : moves.toCharArray()) {
      switch (move) {
        case 'U': y++; break;
        case 'R': x++; break;
        case 'D': y--; break;
        case 'L': x--; break;
      }
    }
    return x == 0 && y == 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/798681246/){:target="_blank"}

# 설명
1. (0, 0) 위치에서 moves에 따라 움직이는 로봇이 원래 위치로 복귀하는지 여부를 검증하는 문제이다.
- 'U'는 로봇이 위로, 'R'은 우측으로, 'D'는  아래로, 'L'은 좌측으로 이동한다.

2. x축과 y축의 위치를 저장할 x와 y를 0으로 초기화한다.

3. moves를 처음부터 끝까지 한 단어씩 반복하여 아래를 수행한다.
- move가 'U'인 경우 y를 증가시키고, 'D'인 경우 y를 감소시킨다.
- move가 'R'인 경우 x를 증가시키고, 'L'인 경우 x를 감소시킨다.

4. 반복이 완료되면 x와 y가 0인지를 검증하여 원점으로 복귀했는지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RobotReturnToOrigin.java){:target="_blank"}에서 확인 가능합니다.