---
title: "Leetcode Java Maximize Score After N Operations"
excerpt: "Leetcode Maximize Score After N Operations Java"
last_modified_at: 2023-05-14T12:40:00
header:
  image: /assets/images/leetcode/count-ways-to-build-good-strings.png
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
[Link](https://leetcode.com/problems/maximize-score-after-n-operations){:target="_blank"}

# 코드
```java
class Solution {

  public int maxScore(int[] nums) {
    int length = nums.length;
    int[][] gcd = new int[length][length];
    for (int i = 0; i < length; i++) {
      for (int j = 0; j < length; j++) {
        gcd[i][j] = this.getGcd(nums[i], nums[j]);
      }
    }
    int[] dp = new int[1 << length];
    for (int i = 0; i < (1 << length); i++) {
      int bits = Integer.bitCount(i);
      if (bits % 2 != 0) {
        continue;
      }
      for (int j = 0; j < length; j++) {
        int jBit = 1 << j;
        if ((i & jBit) > 0) {
          continue;
        }
        for (int k = j + 1; k < length; k++) {
          int kBit = 1 << k;
          if ((i & kBit) > 0) {
            continue;
          }
          dp[i | jBit | kBit] = Math.max(dp[i] + gcd[j][k] * ((bits / 2) + 1), dp[i | jBit | kBit]);
        }
      }
    }
    return dp[(1 << length) - 1];
  }

  private int getGcd(int m, int n) {
    if (n == 0) {
      return m;
    } else {
      return this.getGcd(n, m % n);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximize-score-after-n-operations/submissions/950006270/){:target="_blank"}

# 설명
1. $2 \times n$ 크기의 정수 배열인 nums를 이용하여 i번째 작업(1-인덱스)에서 아래를 수행하여 최대 점수를 반환하는 문제이다.
- x와 y 두 원소를 골라서 $i \times gcd(x, y)$의 점수를 받는다.
- nums에서 x와 y를 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- gcd는 각 조합에 대한 최대 공약수를 저장할 변수로, $length \times length$ 크기로 초기화 하여 모든 값에 대한 최대 공약수를 넣어준다.
- dp는 최대 점수를 구하기 위한 변수로, 1의 비트를 length번 좌측으로 이동시킨 크기로 초기화한다.

3. 0부터 dp의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- bits에 i의 1 비트 수를 넣어주고, 해당 비트가 짝수가 아니라면 다음 반복을 수행한다.
- 0부터 length 미만까지 j를 증가시키며 다음을 수행한다.
- jBit에 1의 비트를 j번 좌측으로 이동시킨 이동시킨 값을 넣어준다.
- i와 jBit의 AND 비트 연산 결과가 0보다 큰 경우, 다음 반복을 수행한다.
- $j + 1$부터 length 미만까지 k를 증가시키며 아래를 수행한다.
  - kBit에 1의 비트를 k번 좌측으로 이동시킨 이동시킨 값을 넣어준다.
  - i와 kBit의 AND 비트 연산 결과가 0보다 큰 경우, 다음 반복을 수행한다.
  - dp의 i, jBit, kBit의 OR 비트 연산 결과의 위치에 대한 값에 해당 값과 $dp[i] + gcd[j][k] \times (\frac{bits}{2} + 1)$인 i번째 작업 결과 중 큰 값을 넣어준다.

4. 반복이 완료되면 dp의 마지막 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximizeScoreAfterNOperations.java){:target="_blank"}에서 확인 가능합니다.