---
title: "Leetcode Java Domino and Tromino Tiling"
excerpt: "Leetcode - 'Domino and Tromino Tiling' 문제 Java 풀이"
last_modified_at: 2023-01-01T17:40:00
header:
  image: /assets/images/leetcode/domino-and-tromino-tiling.png
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
[Link](https://leetcode.com/problems/domino-and-tromino-tiling){:target="_blank"}

# 코드
```java
class Solution {

  public int numTilings(int n) {
    if (n < 3) {
      return n;
    }
    long[] dp = new long[n + 1];
    dp[0] = 1;
    dp[1] = 1;
    dp[2] = 2;
    for (int idx = 3; idx < n + 1; idx++) {
      dp[idx] = ((2 * dp[idx - 1]) + dp[idx - 3]) % 1000000007;
    }
    return (int) dp[n];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/domino-and-tromino-tiling/submissions/868977113/){:target="_blank"}

# 설명
1. $2 \times 1$의 도미노 타일과 'ㄱ'자 모양을 좌우 반전시킨 트로미노 타일을 이용하여 $2 \times n$ 크기의 보드에 타일을 붙이는 방법의 수를 구하는 문제이다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. n이 3 미만인 경우, 붙일 수 있는 타일의 수가 n과 동일하므로 n을 주어진 문제의 결과로 반환한다.

3. dp는 각 방법의 수를 저장할 배열로, 각 계산에 overflow를 방지하기 위해 long 형태의 $n + 1$ 크기로 초기화하고 처음 세 값을 1, 1, 2로 넣어준다.

4. 3부터 $n + 1$까지 idx를 증가시키며 아래를 수행한다.
- dp의 idx번째 위치에 그 전 위치 값의 두 배와 dp의 $idx - 3$번째 값을 더한 값에 모듈러 $10^9 + 7$을 수행한 결과를 넣어준다.
  - 아래의 각 경우를 이용하여 경우의 수 계산을 수행하면 $2 \times 4$의 크기인 보드부터 규칙이 나타난다.
  - $dp[1] = 1$
  - $dp[2] = 2$
  - $dp[3] = 5$
  - $dp[4] = 11 = dp[3] \times 2 + dp[1]$
  - $dp[5] = 24 = dp[4] \times 2 + dp[2]$

5. 반복이 완료되면 dp의 n번째 값을 int형으로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DominoAndTrominoTiling.java){:target="_blank"}에서 확인 가능합니다.