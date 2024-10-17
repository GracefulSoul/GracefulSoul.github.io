---
title: "Leetcode Java Escape The Ghosts"
excerpt: "Leetcode - 'Escape The Ghosts' 문제 Java 풀이"
last_modified_at: 2022-12-31T11:20:00
header:
  image: /assets/images/leetcode/escape-the-ghosts.png
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
[Link](https://leetcode.com/problems/escape-the-ghosts){:target="_blank"}

# 코드
```java
class Solution {

  public boolean escapeGhosts(int[][] ghosts, int[] target) {
    int distance = Math.abs(target[0]) + Math.abs(target[1]);
    for (int[] ghost : ghosts) {
      if (distance >= Math.abs(target[0] - ghost[0]) + Math.abs(target[1] - ghost[1])) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/escape-the-ghosts/submissions/868347589/){:target="_blank"}

# 설명
1. [0, 0]에서 시작해서 귀신들의 위치가 저장된 ghosts의 귀신들보다 빠르게 target에 도달할 수 있는지 검증하는 문제이다.
- 모든 이동은 상하좌우로 1칸씩 이동 가능하다.

2. distance는 현재 위치인 [0, 0]에서 target까지 거리를 저장하기 위한 변수로, target의 x축과 y축의 절댓값의 합을 넣어준다.

3. ghosts의 모든 값을 ghost에 넣어 아래를 검증한다.
- distance가 target과 ghost의 x축 y축 차이의 절댓값의 합보다 큰 경우, 귀신이 target에 더 빠르게 도달하므로 false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 귀신들보다 빠르게 target에 도달 가능하므로 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EscapeTheGhosts.java){:target="_blank"}에서 확인 가능합니다.