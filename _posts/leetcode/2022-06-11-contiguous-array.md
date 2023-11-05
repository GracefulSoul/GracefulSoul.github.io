---
title: "Leetcode Java Contiguous Array"
excerpt: "Leetcode Contiguous Array Java"
last_modified_at: 2022-06-11T11:00:00
header:
  image: /assets/images/leetcode/contiguous-array.png
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
[Link](https://leetcode.com/problems/contiguous-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMaxLength(int[] nums) {
    int length = nums.length;
    int[] dp = new int[2 * length + 1];
    Arrays.fill(dp, -2);
    dp[length] = -1;
    int result = 0;
    int index = length;
    for (int idx = 0; idx < length; idx++) {
      index += nums[idx] == 0 ? -1 : 1;
      if (dp[index] >= -1) {
        result = Math.max(result, idx - dp[index]);
      } else {
        dp[index] = idx;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/719265380/){:target="_blank"}

# 설명
1. 0과 1의 조합으로 연속되어 이루어진 가장 긴 부분 배열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- dp는 길이를 계산에 활용하기 위한 배열로, $2 \times length + 1$ 크기로 초기화 하고 nums의 length 위치에는 -1을 나머지는 -2를 넣어준다.
  - nums가 1로만 이루어져 있을 경우, nums의 위치에서 증가하여 계산하기 때문에 nums의 길이를 중심으로 좌우의 공간을 맞춰주고 -1 낮은 값으로 초기화한다.
- result는 0과 1의 조합으로 연속되어 이루어진 가잔 긴 부분 배열의 길이를 넣을 변수로, 0으로 초기화한다.
- index는 0과 1의 밸런스를 맞춰 계산하기 위한 가중치로, length로 초기화한다.

3. 0부터 nums의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- count에 nums의 idx가 0이면 -1을, 1이면 1을 더해준다.
- dp의 index번째 값이 -1보다 크거나 같은 경우, result에 result와 $idx - dp[index]$ 값 중 큰 값을 넣어준다.
  - 단순히 dp[index]의 값은 위치에 대한 보정 값으로, $idx - dp[index]$는 idx번째까지 [0, 1] 혹은 [1, 0]의 조합의 반복 횟수를 나타낸다.
- dp의 index번째 값이 -1보다 작은 경우, dp의 index번째 값에 idx를 넣어준다.

4. 반복이 완료되면 가장 긴 부분 배열의 길이를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ContiguousArray.java){:target="_blank"}에서 확인 가능합니다.