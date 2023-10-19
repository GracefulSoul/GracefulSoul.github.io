---
title: "Leetcode Java Check Max Consecutive Ones III"
excerpt: "Leetcode Max Consecutive Ones III Java"
last_modified_at: 2023-10-19T19:15:00
header:
  image: /assets/images/leetcode/max-consecutive-ones-iii.png
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
[Link](https://leetcode.com/problems/max-consecutive-ones-iii){:target="_blank"}

# 코드
```java
class Solution {

  public int longestOnes(int[] nums, int k) {
    int i = 0;
    int j = 0;
    while (j < nums.length) {
      if (nums[j++] == 0) {
        k--;
      }
      if (k < 0 && nums[i++] == 0) {
        k++;
      }
    }
    return j - i;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/max-consecutive-ones-iii/submissions/1079085621/){:target="_blank"}

# 설명
1. nums 내 k개의 0을 1로 전환할 때, 가장 긴 연속된 1의 갯수를 구하는 문제이다.

2. i와 j는 1의 시작과 종료의 위치를 저장할 변수로, 둘 다 0으로 초기화한다.

3. j가 nums의 길이 미만일 때 까지 아래를 반복한다.
- nums[j]의 값이 0인 경우, k를 감소시킨 후 모든 경우 j를 증가시켜 위치를 이동시켜준다.
- k가 0보다 작으면서 nums[i]의 값이 0인 경우, k를 증가시켜 이전 감소시킨 전환 갯수를 반환한 후 모든 경우 i를 증가시켜 시작 위치를 이동시켜준다.

4. 반복이 완료되면 $j - i$인 가장 긴 연속된 1의 갯수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxConsecutiveOnesIII.java){:target="_blank"}에서 확인 가능합니다.