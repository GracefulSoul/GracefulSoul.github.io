---
title: "Leetcode Java Chalkboard XOR Game"
excerpt: "Leetcode Chalkboard XOR Game Java"
last_modified_at: 2023-01-19T19:10:00
header:
  image: /assets/images/leetcode/chalkboard-xor-game.png
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
[Link](https://leetcode.com/problems/chalkboard-xor-game){:target="_blank"}

# 코드
```java
class Solution {

  public boolean xorGame(int[] nums) {
    int n = 0;
    for (int num : nums) {
      n ^= num;
    }
    return n == 0 || nums.length % 2 == 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/chalkboard-xor-game/submissions/881125248/){:target="_blank"}

# 설명
1. 엘리스와 밥이 순차적으로 nums 내 임의 숫자를 제거하고 남은 숫자들의 XOR 비트 연산을 수행하다가 밥이 0이 되어 엘리스가 이기는 게임인지 검증하는 문제이다.

2. n은 XOR 비트 연산을 수행한 결과를 저장할 변수로, 0으로 초기화한다.

3. nums의 모든 숫자들을 num에 넣어 아래를 반복한다.
- n에 n과 num의 XOR 비트 연산의 결과를 넣어준다.

4. n이 0이거나 nums의 길이가 짝수이면 true를, 아니면 false를 주어진 문제의 결과로 반환한다.
- 상대가 지게 만드는 경우는, 다음 턴에 nums의 길이가 홀수인 동일 숫자들을 남기는 것이다.
- 아래의 두 경우를 합치면 밥이 어떤 선택을 하던지 엘리스는 반드시 지지 않는 선택을 하여 이길 수 있다.
  - nums 내 모든 숫자들이 같지 않다면, 상대는 절대 지지않는 숫자를 지울 수 있다.
  - 숫자가 모두 같으며 nums 내 숫자의 개수가 짝수인 경우, 상대가 이기게 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ChalkboardXORGame.java){:target="_blank"}에서 확인 가능합니다.