---
title: "Leetcode Java Minimum Swaps To Make Sequences Increasing"
excerpt: "Leetcode Minimum Swaps To Make Sequences Increasing Java"
last_modified_at: 2023-01-12T21:15:00
header:
  image: /assets/images/leetcode/minimum-swaps-to-make-sequences-increasing.png
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
[Link](https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing){:target="_blank"}

# 코드
```java
class Solution {

  public int minSwap(int[] nums1, int[] nums2) {
    int swap = 1;
    int fix = 0;
    for (int idx = 1; idx < nums1.length; idx++) {
      if (nums1[idx - 1] >= nums2[idx] || nums2[idx - 1] >= nums1[idx]) {
        swap++;
      } else if (nums1[idx - 1] >= nums1[idx] || nums2[idx - 1] >= nums2[idx]) {
        int temp = swap;
        swap = fix + 1;
        fix = temp;
      } else {
        int min = Math.min(swap, fix);
        swap = min + 1;
        fix = min;
      }
    }
    return Math.min(swap, fix);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-swaps-to-make-sequences-increasing/submissions/876758394/){:target="_blank"}

# 설명
1. num1과 num2의 값들이 점층적으로 증가하는 값의 배열로 만들기 위해서 같은 위치의 값을 바꾸는 최소 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- swap은 nums1과 nums2의 동일 위치 값을 바꾸기 위한 최소 횟수를 저장할 변수로, 현 위치의 최소 변경 횟수인 1로 초기화한다.
- fix는 nums1과 nums2의 동일 위치 값을 바꾸지 않는 최소 횟수를 저장할 변수로, 현 위치의 최소 고정 횟수인 0으로 초기화한다.

3. 1부터 nums1의 길이 미만까지 idx를 증가시키며 아래를 수행한다.
- 아래의 경우 중 하나라도 만족하면 두 배열 내 idx번째 값을 바꾸어 swap을 증가시킨다.
  - nums1의 $idx - 1$번째 값이 nums2의 idx번째 값보다 크거나 같은 경우.
  - nums2의 $idx - 1$번째 값이 nums1의 idx번째 값보다 크거나 같은 경우.
- 위의 경우가 아니면서 아래의 경우 중 하나라도 만족하면 temp에 swap 값을 임시 저장 후 swap에 fix보다 1 큰 값을 넣고, fix에 temp를 넣어준다.
  - nums1 혹은 nums2의 idx번째 값이 이전 값보다 크거나 같은 경우.
- 위의 두 경우가 아니라면 변경하거나 변경하지 않아도 되므로, min에 swap과 fix 중 작은 값을 임시 저장 후 swap에 $min + 1$을 fix에 min을 넣어준다.

4. 반복이 완료되면 swap과 fix 중 작은 값을 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumSwapsToMakeSequencesIncreasing.java){:target="_blank"}에서 확인 가능합니다.