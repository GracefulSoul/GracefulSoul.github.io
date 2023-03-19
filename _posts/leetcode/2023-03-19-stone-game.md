---
title: "Leetcode Java Stone Game"
excerpt: "Leetcode Stone Game Java"
last_modified_at: 2023-03-19T11:30:00
header:
  image: /assets/images/leetcode/stone-game.png
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
[Link](https://leetcode.com/problems/stone-game){:target="_blank"}

# 코드
```java
class Solution {

  public boolean stoneGame(int[] piles) {
    int sum = 0;
    int total = 0;
    for (int pile : piles) {
      total += pile;
    }
    int left = 0;
    int right = piles.length - 1;
    while (left <= right) {
      if (piles[left] > piles[right]) {
        sum += piles[left++];
      } else {
        sum += piles[right--];
      }
    }
    return sum > total / 2;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/stone-game/submissions/917864497/){:target="_blank"}

# 설명
1. piles에 저장된 돌의 수를 앞과 뒤에서 번갈아가며 가져갈 때 처음 시작하는 사람이 이길 수 있는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 처음 시작하는 사람이 가져간 돌의 숫자를 저장할 변수로, 0으로 초기화한다.
- total은 piles의 모든 돌의 수를 저장할 변수로, piles를 반복하여 모든 값을 더해준다.
- left와 right는 piles의 앞과 뒤의 위치를 저장할 변수로, piles의 처음과 끝의 위치를 넣어 초기화한다.

3. left가 right 이하일 때 까지 아래를 반복한다.
- piles의 left번째 돌의 수가 right번째 돌의 수보다 큰 경우, sum에 piles의 left번째 돌의 수를 더해주고 left를 증가시킨다.
- 위의 경우가 아니라면, sum에 piles의 right번째 돌의 수를 더해주고 right를 감소시킨다.

4. sum이 total의 절반 이상의 돌을 가졌는지 검증한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StoneGame.java){:target="_blank"}에서 확인 가능합니다.