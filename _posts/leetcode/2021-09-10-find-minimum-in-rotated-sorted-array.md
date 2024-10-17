---
title: "Leetcode Java Find Minimum in Rotated Sorted Array"
excerpt: "Leetcode - 'Find Minimum in Rotated Sorted Array' 문제 Java 풀이"
last_modified_at: 2021-09-10T12:00:00
header:
  image: /assets/images/leetcode/find-minimum-in-rotated-sorted-array.png
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
[Link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMin(int[] nums) {
    int left = 0;
    int right = nums.length - 1;
    while (left < right) {
      int mid = (left + right) / 2;
      if (nums[mid] > nums[right]) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return nums[left];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/552314868/){:target="_blank"}

# 설명
1. 주어진 배열 nums를 n번 회전한 배열로, 오름차순으로 정렬되었을 때 최소 숫자를 탐색하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- left는 nums 배열의 시작 index로, 이진 탐색에 사용될 변수이다.
- right는 nums 배열의 마지막 index로, 이진 탐색에 사용될 변수이다.

3. left가 right보다 작을 때 까지 반복하여 left에 배열의 최소값의 index를 넣어준다.
- 중앙값인 mid는 $frac{(left + right)}{2}$ 값으로 넣어 nums[mid]의 값과 nums[right]의 값 중 어느 값이 큰지 검증한다.
  - nums[mid]의 값이 클 경우, left에 $mid + 1$를 넣어 탐색 구간을 좁혀준다.
  - nums[right]의 값이 크거나 같을 경우, right에 mid를 넣어 탐색 구간을 좁혀준다.

4. 반복이 완료되면 오름차순 정렬을 수행했을 경우 최소값이 되는 nums[left]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindMinimumInRotatedSortedArray.java){:target="_blank"}에서 확인 가능합니다.