---
title: "Leetcode Median of Two Sorted Arrays"
excerpt: "Leetcode Median of Two Sorted Arrays 풀이"
last_modified_at: 2021-04-12T20:00:00
header:
  image: /assets/images/leetcode/median-of-two-sorted-arrays
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://leetcode.com/problems/median-of-two-sorted-arrays/)

# 코드
```java
class Solution {

	public double findMedianSortedArrays(int[] nums1, int[] nums2) {
		int[] nums = mergeNums(nums1, nums2);
		int mid = nums.length / 2;
		return nums.length % 2 == 0 ? (double) (nums[mid - 1] + nums[mid]) / 2 : nums[mid];
	}
	
	private int[] mergeNums(int[] nums1, int[] nums2) {
		int[] mergeNums = new int[nums1.length + nums2.length];
		int idx1 = 0;
		int idx2 = 0;
		for (int idx = 0; idx < mergeNums.length; idx++) {
			if (idx1 < nums1.length && (idx2 >= nums2.length || nums1[idx1] <= nums2[idx2])) {
				mergeNums[idx] = nums1[idx1];
				idx1++;
			} else if (idx2 < nums2.length && (idx1 >= nums1.length || nums1[idx1] > nums2[idx2])) {
				mergeNums[idx] = nums2[idx2];
				idx2++;
			}
		}
		return mergeNums;
	}

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/479212877/)

# 설명
1. 주어진 두 배열의 중앙값을 찾기 위해서 하나의 배열로 합친다.
	- 두 배열은 임의의 정렬된 배열이므로, 각 배열을 확인하여 추가하여야 한다.
	- 한 배열의 크기가 다른 배열보다 작을 수 있으므로, 그 부분을 감안하여야 한다.

2. 합친 배열의 중앙값을 문제의 결과로 반환한다.
	- 배열의 크기가 홀수일 경우, 가운데 있는 값이 중앙값이다.
	- 배열의 크가기 짝수일 경우, 가운데 있는 두 값의 평균이 중앙값이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MedianOfTwoSortedArrays.java)에서 확인 가능합니다.