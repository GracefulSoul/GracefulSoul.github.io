---
title: "Leetcode Java Elimination Game"
excerpt: "Leetcode - 'Elimination Game' 문제 Java 풀이"
last_modified_at: 2022-02-18T17:00:00
header:
  image: /assets/images/leetcode/elimination-game.png
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
[Link](https://leetcode.com/problems/elimination-game/){:target="_blank"}

# 코드
```java
class Solution {

  public int lastRemaining(int n) {
    if (n == 1) {
      return n;
    } else {
      return 2 * ((n / 2) + 1 - this.lastRemaining(n / 2));
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/643748283/){:target="_blank"}

# 설명
1. 1부터 주어진 숫자 n까지 숫자를 나열하여 아래의 법칙으로 숫자들을 제거하여 남은 하나의 정수를 반환하는 문제이다.
- 처음은 왼쪽에서 오른쪽으로, 다음은 오른쪽에서 왼쪽으로 번갈아가며 한 자리 씩 넘어가며 제거한다.
- 예를 들어 n이 5인 경우, <b>1</b>, 2, <b>3</b>, 4, <b>5</b> -> 2, <b>4</b> -> 2가 결과가 된다.
- 해당 문제는 [Josephus Problem](https://en.wikipedia.org/wiki/Josephus_problem){:target="_blank"}과 유사한 문제이다.

2. n의 경우에 따라 재귀 호출을 수행하여 결과를 반환한다.
- n이 1인 경우, n을 반환한다.
- n이 1이 아닌 경우, $\frac{2 + n}{2}$에 $\frac{n}{2}$로 재귀 호출 수행한 결과를 빼서 해당 결과의 2배를 반환한다.
  - 위는 $2 \times (\frac{n}{2} + 1 - this.lastRemaining(\frac{n}{2}))$로 표현한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EliminationGame.java){:target="_blank"}에서 확인 가능합니다.