---
title: "Leetcode Java Maximum Average Subarray I"
excerpt: "Leetcode Maximum Average Subarray I Java"
last_modified_at: 2022-09-01T20:20:00
header:
  image: /assets/images/leetcode/maximum-average-subarray-i.png
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
[Link](https://leetcode.com/problems/maximum-average-subarray-i/){:target="_blank"}

# 코드
```java
class Solution {

  public double findMaxAverage(int[] nums, int k) {
    long sum = 0;
    long max = Long.MIN_VALUE;
    for (int idx = 0; idx < nums.length; idx++) {
      sum += nums[idx];
      if (idx > k - 1) {
        sum -= nums[idx - k];
      }
      if (idx >= k - 1) {
        max = Math.max(max, sum);
      }
    }
    return (double) max / k;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/788746584/){:target="_blank"}

# 설명
1. nums 내 k개의 연속된 값들의 평균이 최대인 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 nums 내 k개의 연속된 값들을 더한 결과를 저장할 변수로, 0으로 초기화한다.
- max는 nums 내 k개의 연속된 값들의 평균이 최대인 값을 저장할 변수로, 0으로 초기화한다.

3. 0부터 nums의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- sum에 nums의 idx번째 값을 더해준다.
- idx가 $k - 1$보다 큰 경우, sum에 nums의 $idx - k$번째 값을 빼주어 연속된 k개 합을 유지한다.
- idx가 $k - 1$보다 크거나 같은 경우, max에 max와 sum 중 큰 값을 넣어준다.

4. 반복이 완료되면 max를 실수형으로 형 변환 후 $\frac{max}{k}$의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumAverageSubarrayI.java){:target="_blank"}에서 확인 가능합니다.