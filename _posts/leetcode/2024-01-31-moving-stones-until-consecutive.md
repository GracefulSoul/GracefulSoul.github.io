---
title: "Leetcode Java Moving Stones Until Consecutive"
excerpt: "Leetcode Moving Stones Until Consecutive Java"
last_modified_at: 2024-01-31T19:50:00
header:
  image: /assets/images/leetcode/moving-stones-until-consecutive.png
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
[Link](https://leetcode.com/problems/moving-stones-until-consecutive){:target="_blank"}

# 코드
```java
class Solution {

  public int[] numMovesStones(int a, int b, int c) {
    int[] stones = { a, b, c };
    Arrays.sort(stones);
    if (stones[2] - stones[0] == 2) {
      return new int[] { 0, 0 };
    } else if (Math.min(stones[1] - stones[0], stones[2] - stones[1]) <= 2) {
      return new int[] { 1, stones[2] - stones[0] - 2 };
    } else {
      return new int[] { 2, stones[2] - stones[0] - 2 };
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/moving-stones-until-consecutive/submissions/1161912635/){:target="_blank"}

# 설명
1. a, b, c의 돌 세 개를 아래의 규칙으로 게임을 진행할 때, [최소 이동 수, 최대 이동 수]를 배열로 반환하는 문제이다.
- x < y < z인 세 돌이 존재할 때, x 혹은 z의 돌을 이용하여 x < k < z를 만족하는 y가 아닌 k 위치로 돌을 이동할 수 있다.

2. stones는 a, b, c 세 돌의 위치를 저장할 변수로, 정수 배열에 넣어 오름차순 정렬해준다.

3. 아래의 규칙을 만족하는 경우, 각 경우에 따른 값을 주어진 문제의 결과로 반환한다.
- $stones[2] - stones[0]$이 2인 a, b, c 세 돌이 붙어있는 경우, 모든 이동이 불가능하므로 [0, 0] 배열을 주어진 문제의 결과로 반환한다.
- $stones[1] - stones[0]$ 혹은 $stones[2] - stones[1]$의 결과가 2 이하인 경우, [1, $stones[2] - stones[0] - 2$] 배열을 주어진 문제의 결과로 반한한다.
  - 두 경우 중 하나만 2 이하인 경우, a와 c 돌 중 하나만 b와 인접하므로 최소 이동 횟수는 한 돌만 이동하는 1이 된다.
  - 최대 이동 횟수는 가장 우측에 있는 돌의 위치와 좌측에 있는 돌의 위치의 이동 경우인 $stones[2] - stones[0] - 1$과 b 돌의 위치인 1을 추가로 뺀 경우가 된다.
- 위의 경우가 아니라면, [2, $stones[2] - stones[0] - 2$] 배열을 주어진 문제의 결과로 반한한다.
  - 위 두 경우를 모두 만족하지 않으면 a, b, c 세 돌의 사이의 간격이 존재하므로, a와 c를 이동하는 최소 2번의 이동 횟수가 존재한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MovingStonesUntilConsecutive.java){:target="_blank"}에서 확인 가능합니다.