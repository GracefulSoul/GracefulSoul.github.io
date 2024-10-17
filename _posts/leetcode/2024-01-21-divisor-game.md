---
title: "Leetcode Java Divisor Game"
excerpt: "Leetcode Easy - 'Divisor Game' 문제 Java 풀이"
last_modified_at: 2024-01-21T12:00:00
header:
  image: /assets/images/leetcode/divisor-game.png
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
[Link](https://leetcode.com/problems/divisor-game){:target="_blank"}

# 코드
```java
class Solution {

	public boolean divisorGame(int n) {
		return n % 2 == 0;
	}

}
```

# 결과
[Link](https://leetcode.com/problems/divisor-game/submissions/1152118125/){:target="_blank"}

# 설명
1. 엘리스와 밥이 아래의 규칙대로 게임을 수행할 때, 엘리스가 이기는지 검증하는 문제이다.
- 0 < x < n를 만족할 때, n % x == 0인 임의의 x를 선택하여 n을 $n - x$로 바꾸어준다.
- 플레이어가 더 이상 수행이 불가능한 n이 0이 되는 경우, 게임에서 지게 된다.

2. n이 짝수인지를 검증하여 해당 결과를 주어진 문제의 결과로 반한환다.

# 해설
- n의 각 경우에 대해서 확인해보자.
  - n이 1인 경우, 1을 선택하면서 바로 지게된다.
  - n이 2인 경우, 1을 선택하면 이기게 된다.
  - n이 3인 경우, 1을 선택하면 밥은 1을 다시 선택하므로 반드시 지게된다.
  - n이 4인 경우, 1을 선택하면 n이 3이 되므로, 밥은 1을 선택하여 이기게된다.
- 위의 각 경우에 대한 시나리오를 기반으로 n이 홀수인 경우에는 지고, 짝수인 경우에는 이기므로 짝수인지 검증한 결과가 주어진 문제의 결과로 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DivisorGame.java){:target="_blank"}에서 확인 가능합니다.