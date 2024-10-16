---
title: "Leetcode Java Longest Subarray of 1's After Deleting One Element"
excerpt: "Leetcode Longest Subarray of 1's After Deleting One Element Java"
last_modified_at: 2023-07-05T19:20:00
header:
  image: /assets/images/leetcode/longest-subarray-of-1s-after-deleting-one-element.png
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
[Link](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element){:target="_blank"}

# 코드
```java
class Solution {

  public int longestSubarray(int[] nums) {
    int i = 0;
    int j = 0;
    for (int k = 1; j < nums.length; j++) {
      if (nums[j] == 0) {
        k--;
      }
      if (k < 0 && nums[i++] == 0) {
        k++;
      }
    }
    return j - i - 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/submissions/986842780/){:target="_blank"}

# 설명
1. 0과 1로 이루어진 nums를 이용하여 하나의 요소를 삭제했을 때 1로만 이루어진 가장 긴 길이를 구하는 문제이다.
- 단, 0으로만 구성되는 경우, 0을 반환한다.

2. i와 j는 하나의 요소를 삭제했을 경우 가장 긴 길이를 구하기 위해 시작과 종료 위치를 구하기 위한 위치 변수로, 둘 다 0으로 초기화한다.

3. k는 제거할 요소의 횟수를 저장할 변수로 1로 초기화하고, j는 nums이 길이 미만까지 j를 증가시키며 아래를 반복한다.
- nums의 j번째 값이 0인 경우 k를 감소시켜 횟수를 차감시킨다.
- k가 0 미만이고 nums의 i번째 값이 0이면 i를 증가시키고다시 최대 길이를 계산해야 하므로, k를 증가시킨다.
  - 단 k가 0 이상인 경우, i를 감소시키지 않는다.

4. 반복이 완료되면 계산된 위치의 차이인 $j - i - 1$인 길이를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestSubarrayOfOnesAfterDeletingOneElement.java){:target="_blank"}에서 확인 가능합니다.