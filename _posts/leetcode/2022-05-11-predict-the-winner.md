---
title: "Leetcode Java Predict the Winner"
excerpt: "Leetcode Predict the Winner Java 풀이"
last_modified_at: 2022-05-11T12:00:00
header:
  image: /assets/images/leetcode/predict-the-winner.png
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
[Link](https://leetcode.com/problems/predict-the-winner/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean PredictTheWinner(int[] nums) {
    int length = nums.length;
    int[] dp = new int[length];
    for (int i = length - 1; i >= 0; i--) {
      for (int j = i; j < length; j++) {
        if (i == j) {
          dp[i] = nums[i];
        } else {
          dp[j] = Math.max(nums[i] - dp[j], nums[j] - dp[j - 1]);
        }
      }
    }
    return dp[length - 1] >= 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/697149513/){:target="_blank"}

# 설명
1. 두 사용자가 nums의 첫 값 혹은 마지막 값을 번갈아가며 자신의 점수에 더하고 선택한 값을 배열에서 제거하는 게임을 진행하는데, 첫 번째 사용자가 이길 수 있는지 여부를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 넣어 보관할 변수이다.
- dp는 nums의 값을 더해서 보관할 배열로, length의 크기로 정의한다.

3. $length - 1$부터 0까지 i를 감소시키고, i부터 length 미만까지 j를 증가시키며 반복을 수행한다.
- i와 j가 동일한 값인 경우, dp의 i번째 위치에 nums의 i번째 값을 넣어 값을 초기화시켜준다.
  - i를 역순으로 수행하는 이유는 이를 위해서이며, 별도 반복문으로 dp의 값을 초기화 하지 않도록 하는 것이다.
- i와 j가 동일하지 않은 경우, nums의 i번째 값에 dp의 j번째 값을 뺀 값과 nums의 j번째 값에 dp의 $j - 1$번째 값을 뺀 값 중 큰 값을 dp의 j번째 위치에 넣어준다.
  - dp[j]는 첫 번쨰 플레이어가 두 번째 플레이어보다 j번째 값 까지 얼마나 많은 점수를 얻을 수 있는지를 나타내므로, i에서 j까지 숫자로 선택하는 경우에 대한 예를 보자.
  - 첫 번째 플레이어가 i번째 값을 선택했을 경우, 두 번째 플레이어보다 $nums[i] - dp[j]$ 의 결과만큼 점수가 높을 수 있다.
  - 첫 번째 플레이어가 j번째 값을 선택했을 경우, 두 번째 플레이어보다 $nums[j] - dp[j - 1]$ 의 결과만큼 점수가 높을 수 있다.
  - 첫 번째 플레이어는 두 경우를 고려하여 더 점수가 높은 값을 선택해야 이길 수 있으므로, 가장 큰 값을 dp의 j번째 위치에 넣어주는 것이다.

4. 반복이 완료되면 dp의 $length - 1$번째 값이 0 이상인지를 검증하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PredictTheWinner.java){:target="_blank"}에서 확인 가능합니다.