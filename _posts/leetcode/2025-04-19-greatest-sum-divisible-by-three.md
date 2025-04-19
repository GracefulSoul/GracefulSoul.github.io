---
title: "Leetcode Java Greatest Sum Divisible by Three"
excerpt: "Leetcode - 'Greatest Sum Divisible by Three' 문제 Java 풀이"
last_modified_at: 2025-04-19T16:40:00
header:
  image: /assets/images/leetcode/greatest-sum-divisible-by-three.png
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
[Link](https://leetcode.com/problems/greatest-sum-divisible-by-three/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSumDivThree(int[] nums) {
    int[] dp = new int[3];
    for (int num : nums) {
      for (int i : Arrays.copyOf(dp, dp.length)) {
        int sum = i + num;
        int remainder = sum % 3;
        dp[remainder] = Math.max(dp[remainder], sum);
      }
    }
    return dp[0];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/greatest-sum-divisible-by-three/submissions/1611252625/){:target="_blank"}

# 설명
1. nums 값들 중 합이 3의 배수가 되도록 하는 최댓값을 계산하는 문제이다.

2. dp는 합계를 3으로 나눈 나머지 값에 해당 하는 위치에 저장할 변수로, 3 크기의 정수 배열로 초기화한다.

3. nums의 각 값을 순차적으로 num에 넣어 아래를 반복한다.
- 현재 dp의 값을 그대로 복제하여 순차적으로 i에 넣어 아래를 반복한다.
  - sum은 $i + num$의 값을, remainder는 sum을 3으로 나눈 나머지 값을 저장한 변수이다.
  - dp[remainder]의 위치에 해당 값과 sum 중 가장 큰 값을 넣어준다.

4. 반복이 완료되면 3의 배수 자리의 최댓값이 저장된 dp[0] 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GreatestSumDivisibleByThree.java){:target="_blank"}에서 확인 가능합니다.