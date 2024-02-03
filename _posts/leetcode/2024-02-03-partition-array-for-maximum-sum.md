---
title: "Leetcode Java Partition Array for Maximum Sum"
excerpt: "Leetcode Partition Array for Maximum Sum Java"
last_modified_at: 2024-02-03T09:30:00
header:
  image: /assets/images/leetcode/partition-array-for-maximum-sum.png
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
[Link](https://leetcode.com/problems/partition-array-for-maximum-sum){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSumAfterPartitioning(int[] arr, int k) {
    int length = arr.length;
    int[] dp = new int[length + 1];
    for (int i = 1; i <= length; i++) {
      int max = 0;
      int sum = 0;
      for (int j = 1; j <= k && i - j >= 0; j++) {
        max = Math.max(max, arr[i - j]);
        sum = Math.max(sum, (max * j) + dp[i - j]);
      }
      dp[i] = sum;
    }
    return dp[length];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/partition-array-for-maximum-sum/submissions/1164349496/){:target="_blank"}

# 설명
1. arr을 이용하여 인접한 값들을 최대 k개까지 해당 숫자들 중 가장 큰 값으로 연속되도록 변환할 때, 배열 내 값들의 합이 가장 큰 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- dp는 배열의 값들을 합한 결과가 가장 큰 값을 계산하기 위한 배열로, $length + 1$ 크기의 정수 배열로 초기화한다.

3. 1부터 length 이하까지 i를 증가시키며 아래를 반복한다.
- max와 sum은 가장 큰 값과 합계를 저장할 변수로, 둘 다 0으로 초기화시킨다.
- 1부터 k 이하이면서 $i - j$가 0보다 클 때까지 j를 증가시키며 아래를 반복한다.
  - max에 이전까지 최댓값인 max와 현재 값인 arr[$i - j$] 중 큰 값을 저장한다.
  - sum에 이전까지 합계인 sum과 현재까지 가장 큰 값을 j번 반복하고 현재 값을 더한 $(max \times j) + dp[i - j]$ 값 중 큰 값을 저장한다.
- dp[i]에 sum을 저장한다.

4. 반복이 완료되면 변환된 배열 내 값들의 합이 최대가 되는 값이 저장된 dp[length]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PartitionArrayForMaximumSum.java){:target="_blank"}에서 확인 가능합니다.