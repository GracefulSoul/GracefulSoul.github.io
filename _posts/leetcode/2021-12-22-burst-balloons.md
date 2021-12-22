---
title: "Leetcode Java Burst Balloons"
excerpt: "Leetcode Burst Balloons Java 풀이"
last_modified_at: 2021-12-22T15:00:00
header:
  image: /assets/images/leetcode/burst-balloons.png
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
[Link](https://leetcode.com/problems/burst-balloons/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxCoins(int[] nums) {
    int length = nums.length;
    int[] numbers = new int[length + 2];
    numbers[0] = 1;
    numbers[length + 1] = 1;
    for (int idx = 0; idx < length; idx++) {
      numbers[idx + 1] = nums[idx];
    }
    int[][] dp = new int[length + 2][length + 2];
    for (int j = 2; j < numbers.length; j++) {
      for (int i = j - 1; i > 0; i--) {
        int max = 0;
        for (int k = i; k < j; k++) {
          max = Math.max(max, dp[i][k] + dp[k + 1][j] + (numbers[i - 1] * numbers[k] * numbers[j]));
        }
        dp[i][j] = max;
      }
    }
    return dp[1][length + 1];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/605377106/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums를 이용하여 풍선터트려 받을 수 있는 최대 코인을 반환하는 문제이다.
- i번째 풍선을 터트리면 $nums[i - 1] \times nums[i] \times nums[i + 1]$ 코인을 받는다.
- $i - 1$ 혹은 $i + 1$의 자리가 배열의 범위를 벗어날 경우, 1의 값이 있다고 가정한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 주어진 배열 num의 길이를 저장할 배열이다.
- numbers는 1번의 두 번째 조건을 만족하기 위해 주어진 nums의 앞 뒤에 1의 값을 추가할 배열로, $length + 2$ 크기로 정의하고 0번째와 $length + 1$번째 값에 1을 넣고 그 가운데는 nums의 값들을 넣어준다.

3. 최대 코인을 산정하기 위해 2차원 배열인 dp를 가로와 세로의 길이가 $length + 2$의 크기로 정의한다.

4. 반복문을 통해 dp에 값을 넣어준다.
- 2부터 numbers의 길이만큼 j를 증가시키며 반복하고, 다시 $j - 1$부터 i가 0보다 클 때까지 i를 감소시켜 반복한다.
  - max에 임시로 0을 넣어주고 i부터 j 이전까지 k를 증가시켜 반복하여 max와 $dp[i][k] + dp[k + 1] + numbers[i - 1] \times numbers[k] \times numbers[j]$의 값중 최대 코인을 찾아 max에 넣어준다.
  - dp[i][j]에 위의 반복을 통해 정해진 max 값을 넣어준다.

5. 반복이 종료되면 최대 코인을 저장한 dp[1][length + 1]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BurstBalloons.java){:target="_blank"}에서 확인 가능합니다.