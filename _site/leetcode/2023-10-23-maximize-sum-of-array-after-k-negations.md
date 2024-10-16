---
title: "Leetcode Java Maximize Sum Of Array After K Negations"
excerpt: "Leetcode Maximize Sum Of Array After K Negations Java"
last_modified_at: 2023-10-23T20:20:00
header:
  image: /assets/images/leetcode/maximize-sum-of-array-after-k-negations.png
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
[Link](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations){:target="_blank"}

# 코드
```java
class Solution {

  public int largestSumAfterKNegations(int[] nums, int k) {
    Arrays.sort(nums);
    for (int i = 0; k > 0 && i < nums.length && nums[i] < 0; i++, k--) {
      nums[i] = -nums[i];
    }
    int result = 0;
    int min = Integer.MAX_VALUE;
    for (int num : nums) {
      result += num;
      min = Math.min(min, num);
    }
    return result - ((k % 2) * min * 2);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/submissions/1082060488/){:target="_blank"}

# 설명
1. nums 내 k개의 값을 음수/양수로 전환하였을 때 nums 내 값들의 합이 최대를 구하는 문제이다.

2. nums의 값들을 오름차순으로 정렬한다.

3. 0부터 nums의 길이 미만까지 i를 증가시키고, k가 0보다 클 때 까지 k를 감소시키며 nums의 i번째 값을 음수/양수 전환한다.

4. 문제 풀이에 필요한 변수를 정의한다.
- result는 최대인 값을 저장할 변수로, 0으로 초기화한다.
- min은 값의 최솟값을 저장할 변수로, 정수의 최댓값으로 초기화한다.

5. nums의 모든 값을 순차적으로 num에 넣어 아래를 반복한다.
- result에 num을 넣고, min에 min과 num 중 작은 값을 넣어준다.

6. result에 $\frac{k}{2} \times min \times 2$의 값을 빼준 값을 주어진 문제의 결과로 반환한다.
- 이미 nums의 모든 값을 result에 넣었으므로 min에 2를 곱해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximizeSumOfArrayAfterKNegations.java){:target="_blank"}에서 확인 가능합니다.