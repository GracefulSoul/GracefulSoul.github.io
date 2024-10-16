---
title: "Leetcode Java Delete and Earn"
excerpt: "Leetcode Delete and Earn Java"
last_modified_at: 2022-11-29T13:20:00
header:
  image: /assets/images/leetcode/delete-and-earn.png
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
[Link](https://leetcode.com/problems/delete-and-earn){:target="_blank"}

# 코드
```java
class Solution {

  public int deleteAndEarn(int[] nums) {
    int[] dp = new int[10001];
    int max = 0;
    for (int num : nums) {
      dp[num] = dp[num] + num;
      max = Math.max(num, max);
    }
    for (int idx = 2; idx <= max; idx++) {
      dp[idx] = Math.max(dp[idx - 1], dp[idx] + dp[idx - 2]);
    }
    return dp[max];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/851530240/){:target="_blank"}

# 설명
1. nums의 idx번째 값을 선택하면 $num[i] - 1$과 $num[i] + 1$의 값들을 배열에서 제거하면서 점수를 획득할 수 있는데, 해당 값이 최대인 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 값을 계산하기 위한 변수로, 정수의 최대 범위의 한계인 10001 크기의 정수 배열로 초기화한다.
- max는 nums 내 최댓 값을 저장하기 위한 변수로, 0으로 초기화한다.

3. nums의 모든 값을 num에 순차적으로 넣어 아래를 반복한다.
- dp의 num번쨰 위치에 해당 위치 값과 num을 더해서 넣어주고, max에 num과 max 중 큰 값을 저장한다.

4. 위의 반복이 완료되면 2부터 max 이하까지 idx를 증가시키며 아래를 반복한다.
- dp의 idx번째 위치에 dp의 $idx - 1$번째 값과 idx와 $idx - 2$번째 값의 합 중 큰 값을 넣어 해당 값을 선택할 경우 얻을 수 있는 포인트를 저장한다.

5. 포인트의 최댓 값이 저장된 dp의 max번째 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteAndEarn.java){:target="_blank"}에서 확인 가능합니다.