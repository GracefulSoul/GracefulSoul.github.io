---
title: "Leetcode Java Largest Positive Integer That Exists With Its Negative"
excerpt: "Leetcode Easy - 'Largest Positive Integer That Exists With Its Negative' 문제 Java 풀이"
last_modified_at: 2024-05-02T18:20:00
header:
  image: /assets/images/leetcode/largest-positive-integer-that-exists-with-its-negative.png
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
[Link](https://leetcode.com/problems/largest-positive-integer-that-exists-with-its-negative/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMaxK(int[] nums) {
    Arrays.sort(nums);
    for (int i = nums.length - 1; i >= 0; i--) {
      if (nums[i] > 0 && Arrays.binarySearch(nums, -nums[i]) >= 0) {
        return nums[i];
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-positive-integer-that-exists-with-its-negative/submissions/1247262016/){:target="_blank"}

# 설명
1. nums 내 음수 부호를 제거한 값의 절댓값이 동일한 값을 찾아 양수로 반환하는 문제이다.
- 단, 값을 찾을 수 없으면 -1을 주어진 문제의 결과로 반환한다.

2. nums를 오름차순 정렬한다.

3. nums의 길이보다 1 작은 값부터 0 이상까지 i를 감소시키며 거꾸로 탐색을 수행한다.
- nums[i]의 값이 0보다 크면서 nums 내 nums[i]의 음수 값이 존재하는 경우, nums[i]의 값을 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 조건을 만족하는 값을 찾을 수 없으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestPositiveIntegerThatExistsWithItsNegative.java){:target="_blank"}에서 확인 가능합니다.