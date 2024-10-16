---
title: "Leetcode Java Last Stone Weight II"
excerpt: "Leetcode Last Stone Weight II Java"
last_modified_at: 2024-03-18T19:20:00
header:
  image: /assets/images/leetcode/last-stone-weight-ii.png
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
[Link](https://leetcode.com/problems/last-stone-weight-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int lastStoneWeightII(int[] stones) {
    int sum = 0;
    for (int stone : stones) {
      sum += stone;
    }
    int[] dp = new int[(sum / 2) + 1];
    for (int i = 0; i < stones.length; i++) {
      for (int j = sum / 2; j >= stones[i]; j--) {
        dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
      }
    }
    return sum - (2 * dp[sum / 2]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/last-stone-weight-ii/submissions/1207110399/){:target="_blank"}

# 설명
1. 돌의 무게가 저장된 stones를 이용하여 아래의 규칙대로 돌을 부술 때, 남은 돌의 무게가 최소가 되는 값을 구하는 문제이다.
- x와 y 두 돌의 무게가 x <= y를 만족할 때, 두 돌을 부순 결과는 아래와 같다.
  - x와 y의 무게가 동일하다면, 두 돌은 파괴된다.
  - x와 y의 무게가 돌일하지 않다면, x는 파괴되고 두 돌의 무게 차이 값의 돌이 남는다.
- 마지막엔 하나의 돌만 남게 되고, 돌이 남아있지 않는다면 주어진 문제의 결과로 0을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 돌의 합계를 저장할 변수로, stones의 모든 돌의 무게를 더해준다.
- dp는 부서진 돌의 무게를 계산하기 위해 사용할 배열로, $\frac{sum}{2} + 1$ 크기의 정수 배열로 초기화한다.

3. 0부터 stones의 길이 미만까지 i를 증가시키고, $\frac{sum}{2}$부터 stones[i] 이상일 때 까지 j를 감소시키며 아래를 반복한다.
- dp[j]에 dp[j]와 dp[$j - stones[i]$]에 stones[i]를 뺀 값 중 큰 값을 넣어준다.

4. 주어진 문제의 결과로 $sum - (2 \times dp[\frac{sum}{2}])$의 값을 주어진 문제의 결과로 반환한다.

# 해설
- 돌은 두 집단을 나누어 부수게 되므로, 계산을 최소화 하기 위해 값의 범위를 $\frac{sum}{2}$로 정하고 dp를 해당 값보다 1 큰 크기로 초기화한다.
- stones의 i는 순차적으로 증가시키고, j는 역순으로 탐색하는 이유는 dp[$j - stones[i]$]의 값에 대해서 $i + 1$번째 돌을 고려하지 않고 계산되었으므로 다시 반복하지 않기 위해서이다.
- 이렇게 남은 돌의 무게가 최소가 되는 값은, stones 내 돌 무게의 합인 sum에서 dp의 마지막 위치에 저장된 절반 범위 내 부서질 돌의 최대 무게인 dp[$\frac{sum}{2}$] 값에 2를 곱한 값을 빼준 값이 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LastStoneWeightII.java){:target="_blank"}에서 확인 가능합니다.