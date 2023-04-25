---
title: "Leetcode Java Smallest Range I"
excerpt: "Leetcode Smallest Range I Java"
last_modified_at: 2023-04-25T18:50:00
header:
  image: /assets/images/leetcode/smallest-range-i.png
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
[Link](https://leetcode.com/problems/smallest-range-i){:target="_blank"}

# 코드
```java
class Solution {

  public int smallestRangeI(int[] nums, int k) {
    int max = nums[0];
    int min = nums[0];
    for (int num : nums) {
      max = Math.max(max, num);
      min = Math.min(min, num);
    }
    return Math.max(0, max - min - (k * 2));
  }

}
```

# 결과
[Link](https://leetcode.com/problems/smallest-range-i/submissions/938894204/){:target="_blank"}

# 설명
1. nums의 모든 값에 [-k, k] 범위의 값을 더했을 때, 최댓값과 최솟값의 차이가 가장 작은 값을 구하는 문제이다.

2. max와 min에 nums의 최댓값과 최솟값을 찾아 넣어준다.

3. 둘의 차이가 가장 작은 임계치는 0이므로, 0과 $(max - k) - (min + k) = max - min - (k \times 2)$ 중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SmallestRangeI.java){:target="_blank"}에서 확인 가능합니다.