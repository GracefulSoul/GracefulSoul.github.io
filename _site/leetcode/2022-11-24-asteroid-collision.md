---
title: "Leetcode Java Asteroid Collision"
excerpt: "Leetcode Asteroid Collision Java"
last_modified_at: 2022-11-24T19:00:00
header:
  image: /assets/images/leetcode/asteroid-collision.png
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
[Link](https://leetcode.com/problems/asteroid-collision){:target="_blank"}

# 코드
```java
class Solution {

  public int[] asteroidCollision(int[] asteroids) {
    int index = -1;
    for (int asteroid : asteroids) {
      boolean alive = true;
      while (alive && asteroid < 0 && index >= 0 && asteroids[index] > 0) {
        alive = asteroids[index] + asteroid < 0;
        if (asteroids[index] + asteroid <= 0) {
          index--;
        }
      }
      if (alive) {
        asteroids[++index] = asteroid;
      }
    }
    return Arrays.copyOf(asteroids, index + 1);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/849056551/){:target="_blank"}

# 설명
1. 연속적으로 소행성의 크기를 저장한 asteroids 배열을 이용하여 살아남은 소행성을 반환하는 문제이다.
- 양수는 오른쪽 음수는 왼쪽으로 이동하는 방향을 나타낸다.
- 양수와 음수로 마주치는 두 소행성의 경우, 크기가 큰 소행성만 살아남는다.
- 양수와 음수로 마주치는 두 소행성의 크기가 같은 경우, 두 소행성 모두 폭발한다.
- 소행성은 모두 같은 속도로 움직이며, 같은 방향으로 움직이는 소행성은 절대 만나지 않는다.

2. index는 살아남은 소행성만 저장한 asteroids 배열을 자르기 위한 위치 변수로, -1로 초기화한다.

3. asteroids 배열을 순서대로 asteroid 변수에 넣어 아래를 반복한다.
- alive는 살아있는 상태를 저장하기 위한 변수로, true로 초기화한다.
- alive가 true로 살아있는 소행성이면서 asteroid인 소행성의 크기가 음수이고 index가 0보다 크면서 asteroids의 index번째 소행성의 크기가 0보다 커서 마주치면 아래를 계속 수행한다.
  - alive에 asteroids의 index번째 소행성의 크기와 asteroid의 합이 0보다 작은지를 여부를 넣어준다.
  - asteroids의 index번째 소행성의 크기와 asteroid의 합이 0보다 같거나 작으면 해당 행성을 제거해야하므로, index를 감소시킨다.
- alive가 true인 살아남는 소행성인 경우, index를 증가시키고 asteroid의 index번째 위치에 해당 소행성의 크기인 asteroid를 넣어준다.

4. 반복이 완료되면 살아남은 소행성을 순차적으로 index번째까지 저장한 asteroids를 $index + 1$ 크기의 새 배열로 복사하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AsteroidCollision.java){:target="_blank"}에서 확인 가능합니다.