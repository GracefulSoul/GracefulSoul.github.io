---
title: "Leetcode Java Find First and Last Position of Element in Sorted Array"
excerpt: "Leetcode Find First and Last Position of Element in Sorted Array Java 풀이"
last_modified_at: 2021-05-18T18:20:00
header:
  image: /assets/images/leetcode/find-first-and-last-position-of-element-in-sorted-array.png
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
[Link](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] searchRange(int[] nums, int target) {
    int first = this.search(nums, target);
    if (first == nums.length || nums[first] != target) {
      return new int[] { -1, -1 };
    } else {
      return new int[] { first, this.search(nums, target + 1) - 1 };
    }
  }

  private int search(int[] nums, int target) {
    int low = 0;
    int high = nums.length;
    while (low < high) {
      int mid = (low + high) / 2;
      if (nums[mid] < target) {
        low = mid + 1;
      } else {
        high = mid;
      }
    }
    return low;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/494715184/){:target="_blank"}

# 설명
1. 주어진 문제는 반드시 $O\log n$의 시간 복잡도로 풀어야 하는 조건을 반드시 명심해야 한다.

2. 이진 탐색을 통해 주어진 배열 nums 안에 존재하는 target 정수가 존재하는 첫번째 index를 탐색한다.
- 0부터 nums의 길이를 기반으로 절반씩 나누어 target의 index를 탐색한다.

3. 첫 탐색 결과 index가 주어진 배열 num의 길이와 같거나, 주어진 배열의 index번째 값이 target과 다른 경우 목표하는 값이 존재하지 않으므로 [-1, -1] 배열을 주어진 문제의 결과로 반환한다.

4. 그렇지 않은 경우, 두 번째 이진 탐색을 target + 1 값으로 탐색하고, 반환된 index에 - 1을 하여 마지막 index를 탐색하여 first 값과 해당 index를 배열로 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindFirstAndLastPositionOfElementInSortedArray.java){:target="_blank"}에서 확인 가능합니다.