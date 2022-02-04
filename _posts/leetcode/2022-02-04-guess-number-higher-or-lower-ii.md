---
title: "Leetcode Java Guess Number Higher or Lower II"
excerpt: "Leetcode Guess Number Higher or Lower II Java 풀이"
last_modified_at: 2022-02-04T13:00:00
header:
  image: /assets/images/leetcode/guess-number-higher-or-lower-ii.png
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
[Link](https://leetcode.com/problems/guess-number-higher-or-lower-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int getMoneyAmount(int n) {
    return this.recursive(new int[n + 1][n + 1], 1, n);
  }

  private int recursive(int[][] dp, int low, int high) {
    if (low >= high) {
      return 0;
    } else if (dp[low][high] > 0) {
      return dp[low][high];
    } else {
      dp[low][high] = Integer.MAX_VALUE;
      int mid = (low + high) / 2;
      for (int idx = mid; idx < high; idx++) {
        int left = this.recursive(dp, low, idx - 1);
        int right = this.recursive(dp, idx + 1, high);
        dp[low][high] = Math.min(dp[low][high], idx + Math.max(left, right));
        if (left >= right) {
          break;
        }
      }
    }
    return dp[low][high];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/634128039/){:target="_blank"}

# 설명
1. 1과 주어진 정수 n 사이의 올바른 숫자를 맞추는 과정 속에 아래의 조건을 통해 선택한 숫자에 관계 없이 승리할 수 있는 최소 금액을 반환하는 문제이다.
- 올바른 숫자를 맞추면 게임에서 승리한다.
- 잘못된 숫자를 맞추면 고른 숫자가 더 높거나 낮은지를 알려주고, 해당 숫자만큼의 달러를 지불하게 된다.

2. dp를 [$n + 1$][$n + 1$] 크기로 재귀 호출을 사용하여 1부터 n까지 숫자로 최소 금액을 탐색한다.

3. low가 high보다 크거나 같을 경우 탐색 범위를 벗어났으므로, 0을 반환한다.

4. dp[low][high]의 값이 0보다 큰 경우 해당 위치의 값은 이미 탐색이 되었으므로, 해당 값을 반환한다.

5. 3번과 4번의 경우가 아닌 경우, 아래를 수행한다.
- dp[low][high]에 정수의 가장 큰 값을 넣어주고, mid에 $\frac{low + high}{2}$의 값을 넣어준다.
- mid부터 high까지 idx를 증가시키며 반복을 수행한다.
  - left에 low와 high에 $idx - 1$를 넣어 재귀 호출을 수행한 결과를 넣어준다.
  - right에 low에 $idx + 1$과 high를 넣어 재귀 호출을 수행한 결과를 넣어준다.
  - dp[low][high]에 dp[low][high]의 값과 left와 right 중 큰 값에 idx를 더한 값 중 작은 값을 넣어준다.
  - left가 right보다 크거나 같은 경우 반복을 중단한다.

6. 반복이 완료되면 dp[low][high] 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GuessNumberHigherOrLowerII.java){:target="_blank"}에서 확인 가능합니다.