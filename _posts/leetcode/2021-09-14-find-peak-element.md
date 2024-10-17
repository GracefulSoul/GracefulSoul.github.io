---
title: "Leetcode Java Find Peak Element"
excerpt: "Leetcode - 'Find Peak Element' 문제 Java 풀이"
last_modified_at: 2021-09-14T12:00:00
header:
  image: /assets/images/leetcode/find-peak-element.png
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
[Link](https://leetcode.com/problems/find-peak-element/){:target="_blank"}

# 코드
```java
class Solution {

  public int findPeakElement(int[] nums) {
    int length = nums.length;
    if (length == 1) {
      return 0;
    }
    int left = 0;
    int right = length - 1;
    while (left + 1 < right) {
      int mid = left + (right - left) / 2;
      if (nums[mid] < nums[mid + 1]) {
        left = mid;
      } else {
        right = mid;
      }
    }
    return nums[left] > nums[right] ? left : right;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/554511647/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums의 가장 높은 값을 찾아 index를 반환하는 문제이다.

2. 주어진 정수 배열의 크기가 1인 경우, 탐색할 필요가 없으므로 0을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- left는 left -> right 방향으로 탐색하기 위한 변수로, 0으로 초기화한다.
- right는 right -> left 방향으로 탐색하기 위한 변수로, 주어진 배열인 nums의 크기로 초기화한다.

4. $left + 1$이 right보다 작을 때까지 반복하여 최고 값이 되는 위치를 탐색한다.
- 임시 변수인 mid에 $left + frac{right - left}{2}$를 넣고 nums[mid]의 값과 nums[mid + 1]의 값을 비교한다.
  - nums[mid]의 값이 nums[mid + 1]의 값보다 작을 경우, left에 mid를 넣어준다.
  - nums[mid]의 값이 nums[mid + 1]의 값보다 크거나 같은 경우, right에 mid를 넣어준다.

5. 반복이 완료되면 nums[left]의 값과 nums[right]의 값을 비교하여 주어진 문제의 결과로 반환한다.
- nums[left]가 nums[right]의 값보다 큰 경우, left를 주어진 문제의 결과로 반환한다.
- nums[left]가 nums[right]의 값보다 작거나 같은 경우, right를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindPeakElement.java){:target="_blank"}에서 확인 가능합니다.