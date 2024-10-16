---
title: "Leetcode Java Minimum Cost to Merge Stones"
excerpt: "Leetcode Minimum Cost to Merge Stones Java"
last_modified_at: 2023-10-05T20:35:00
header:
  image: /assets/images/leetcode/minimum-cost-to-merge-stones.png
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
[Link](https://leetcode.com/problems/minimum-cost-to-merge-stones){:target="_blank"}

# 코드
```java
class Solution {

  public int mergeStones(int[] stones, int k) {
    int length = stones.length;
    if ((length - 1) % (k - 1) > 0) {
      return -1;
    }
    int[] sum = new int[length + 1];
    for (int i = 0; i < length; i++) {
      sum[i + 1] = sum[i] + stones[i];
    }
    int[][] dp = new int[length][length];
    for (int end = k; end <= length; end++) {
      for (int start = 0; start + end <= length; start++) {
        int max = start + end - 1;
        dp[start][max] = Integer.MAX_VALUE;
        for (int mid = start; mid < max; mid += k - 1) {
          dp[start][max] = Math.min(dp[start][max], dp[start][mid] + dp[mid + 1][max]);
        }
        if ((max - start) % (k - 1) == 0) {
          dp[start][max] += sum[max + 1] - sum[start];
        }
      }
    }
    return dp[0][length - 1];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-cost-to-merge-stones/submissions/1067658174/){:target="_blank"}

# 설명
1. stones 내 연속된 k개의 값을 더해 최후의 하나의 값을 만들기 위한 각 부분 합을 더한 값이 최소가 되는 값을 구하는 문제이다.

2. length는 stones의 길이를 저장한 변수이다.

3. $\frac{length - 1}{k - 1}$의 결과가 정수로 떨어지지 않은 경우, k개씩 값을 더해서 최후의 하나의 값이 되지 않으므로 -1을 주어진 문제의 결과로 반환한다.

4. 문제 풀이에 필요한 변수를 정의한다.
- sum은 각 위치 별 합계를 저장할 변수로, $length + 1$ 크기로 초기화하고 두 번째 위치부터 이전까지 값들의 합을 더해 넣어준다.
- dp는 부분 합을 더한 값이 최소가 되는 값을 찾기 위한 배열로, $length \times length$ 크기의 2차원 배열로 초기화한다.

5. k부터 length 이하까지 end를 증가시키고, 0부터 $start + end$가 length 이하일 때 까지 start를 증가시키며 아래를 반복한다.
- max는 start번째 반복의 최대 위치인 $start + end - 1$을 넣어준다.
- dp[start][max]의 값에 정수의 최댓값을 넣어준다.
- start부터 max 미만까지 mid를 $k - 1$씩 증가시키며 아래를 수행한다.
  - dp[start][max]의 값에 dp[start][max]의 값과 dp[start][mid]의 값에 dp[$mid + 1$][max]의 값을 더한 값 중 작은 값을 넣어준다.
- $\frac{max - start}{k - 1}$의 결과가 정수로 떨어지는 경우, dp[start][max]에 sum[max + 1]의 값에 sum[start]의 값을 뺀 start번째 값에서 max까지의 값의 합을 더해준다.

6. 반복이 완료되면 문제의 조건에 대한 값이 최소가 되는 dp[0][$length - 1$]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumCostToMergeStones.java){:target="_blank"}에서 확인 가능합니다.