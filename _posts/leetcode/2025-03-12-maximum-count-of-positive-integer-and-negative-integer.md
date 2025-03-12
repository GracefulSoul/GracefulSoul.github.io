---
title: "Leetcode Java Maximum Count of Positive Integer and Negative Integer"
excerpt: "Leetcode - 'Maximum Count of Positive Integer and Negative Integer' 문제 Java 풀이"
last_modified_at: 2025-03-12T19:00:00
header:
  image: /assets/images/leetcode/maximum-count-of-positive-integer-and-negative-integer.png
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
[Link](https://leetcode.com/problems/maximum-count-of-positive-integer-and-negative-integer/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumCount(int[] nums) {
    return Math.max(this.binarySearch(nums, 0), nums.length - this.binarySearch(nums, 1));
  }

  private int binarySearch(int[] nums, int target) {
    int left = 0;
    int right = nums.length;
    while (left < right) {
      int mid = left + (right - left) / 2;
      if (nums[mid] < target) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return right;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/submissions/1570090687/){:target="_blank"}

# 설명
1. 오름차순 정렬된 정수 배열인 nums 내 양의 정수와 음의 정수 갯수 중 가장 많은 정수의 갯수를 반환하는 문제이다.

2. 이진 탐색을 수행할 binarySearch(int[] nums, int target) 메서드를 정의한다.
- left와 right는 nums의 위치 탐색을 위한 시작과 종료 위치를 저장할 변수로, 0과 nums의 길이로 초기화한다.
- left가 right 미만일 때 까지 아래를 수행한다.
  - mid에 $left + \frac{right - left}{2}$인 중앙값을 넣어준다.
  - nums[mid]의 값이 target 미만이면 left에 $mid + 1$을, 아니면 right에 mid를 넣어 범위를 좁혀준다.

3. 아래의 두 값 중 큰 값인 가장 많은 정수의 갯수를 주어진 문제의 결과로 반환한다.
- 2번의 binarySearch(int[] nums, int target) 메서드를 nums와 0을 넣어 수행한 음의 정수 갯수.
- nums의 길이에서 2번의 binarySearch(int[] nums, int target) 메서드를 nums와 1을 넣어 수행한 0 이하의 정수 갯수를 뺀 양의 정수 갯수.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumCountOfPositiveIntegerAndNegativeInteger.java){:target="_blank"}에서 확인 가능합니다.