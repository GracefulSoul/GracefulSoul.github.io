---
title: "Leetcode Java Find the Winner of the Circular Game"
excerpt: "Leetcode Medium - 'Find the Winner of the Circular Game' 문제 Java 풀이"
last_modified_at: 2024-07-08T22:50:00
header:
  image: /assets/images/leetcode/find-the-winner-of-the-circular-game.png
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
[Link](https://leetcode.com/problems/find-the-winner-of-the-circular-game/){:target="_blank"}

# 코드
```java
class Solution {

  public int findTheWinner(int n, int k) {
    int result = 0;
    for (int i = 2; i <= n; i++) {
      result = (result + k) % i;
    }
    return result + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/water-bottles/submissions/1312930745/){:target="_blank"}

# 설명
1. n명의 친구들끼리 원형 모양으로 앉아 아래의 규칙을 만족하는 게임을 수행 후 승자를 반환하는 문제이다.
- i번째 친구에서 시계 방향으로 이동하면 1 <= i < n 을 만족하는 $i + 1$번째 친구로 이동하고, n번째 친구에서 시계 방향으로 이동하면 1번째 친구로 이동한다.
- 아래의 게임을 한 명이 남아 승리할 때 까지 반복한다.
  - 첫 번째 친구부터 시작하여 해당 친구를 포함하여 시계 방향으로 k명의 친구를 센다. 단, 동일한 친구를 두 번 이상 셀 수 있다.
  - 마지막 세었던 친구는 게임에서 지고, 자리에서 떠난다.

2. result는 승리할 친구의 위치를 저장할 변수로, 0으로 초기화한다.

3. 게임의 최소 인원인 2부터 총 인원인 n 이하까지 i를 증가시키며, result에 현재 순서인 친구 위치인 result에 세어야 할 k를 더한 후 i로 나눈 나머지 값을 넣어준다.

4. 반복이 완료되면 승리한 친구의 번호인 $result + 1$을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheWinnerOfTheCircularGame.java){:target="_blank"}에서 확인 가능합니다.