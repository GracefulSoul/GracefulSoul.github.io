---
title: "Leetcode Java Reach a Number"
excerpt: "Leetcode - 'Reach a Number' 문제 Java 풀이"
last_modified_at: 2022-12-08T12:30:00
header:
  image: /assets/images/leetcode/reach-a-number.png
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
[Link](https://leetcode.com/problems/reach-a-number){:target="_blank"}

# 코드
```java
class Solution {

  public int reachNumber(int target) {
    target = Math.abs(target);
    int numMoves = 0;
    while (target > 0) {
      target -= ++numMoves; 
    }
    if (target != 0 && target % 2 != 0) {
      while (target % 2 != 0) {
        target -= ++numMoves;
      }
    }
    return numMoves;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reach-a-number/submissions/856419049/){:target="_blank"}

# 설명
1. 0에서 시작하여 target까지 가기 위한 최소한의 이동 횟수를 구하는 문제이다.
- 이동은 좌측(-) 혹은 우측(+)으로 이동이 가능하다.
- 각 이동은 1부터 점층적으로 증가하는 숫자만큼 이동이 가능하다.

2. target에 target의 절댓값을 넣어준다.

3. numMoves를 0으로 초기화 하고, target이 0 이상일 때 까지 numMoves 증가시키고 target에서 빼준다.

4. target이 0이 아니면서, 홀수인 경우 정확히 target에 도달하지 못하므로 아래를 수행한다.
- target이 짝수가 될 때까지 3번과 동일하게 numMoves 증가시키고 target에서 빼주어 이동 횟수를 계산한다.

5. 계산된 최소 이동 횟수인 numMoves를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReachANumber.java){:target="_blank"}에서 확인 가능합니다.