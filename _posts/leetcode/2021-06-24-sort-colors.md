---
title: "Leetcode Java Sort Colors"
excerpt: "Leetcode Sort Colors Java 풀이"
last_modified_at: 2021-06-24T21:20:00
header:
  image: /assets/images/leetcode/sort-colors.png
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
[Link](https://leetcode.com/problems/sort-colors/){:target="_blank"}

# 코드
```java
class Solution {

  public void sortColors(int[] nums) {
    int start = 0;
    int end = nums.length - 1;
    int idx = 0;
    while (idx <= end) {
      switch (nums[idx]) {
        case 0:
          if (nums[start] != 0) {
            this.swap(nums, idx, start);
          }
          start++;
          idx++;
          break;
        case 2:
          if (nums[end] != 2) {
            this.swap(nums, idx, end);
          }
          end--;
          break;
        default:
          idx++;
          break;
      }
    }
  }

  private void swap(int[] nums, int idx1, int idx2) {
    int temp = nums[idx2];
    nums[idx2] = nums[idx1];
    nums[idx1] = temp;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/512530762/){:target="_blank"}

# 설명
1. 각 색상을 나타내는 숫자인 0, 1, 2로 구성된 주어진 배열을 정렬하는 문제이다.

2. 배열의 탐색을 위해 변수들을 정의한다.
- 변수 start는 배열의 첫 인덱스인 0으로 정의한다.
- 변수 end는 배열의 마지막 인덱스인 $nums.length - 1$으로 정의한다.
- 변수 idx는 포인터 역할을 하며, 배열의 첫 인덱스인 0으로 선언한다.

3. 변수 idx의 값이 end가 될 때 까지 반복하여 주어진 배열을 정렬하여 문제를 해결한다.
- nums[idx]의 값이 0인 경우, nums[start]의 값이 0이 아닌 값이면 배열 nums의 idx번째 값과 바꾸고 start와 idx의 값을 증가시킨다.
- nums[idx]의 값이 2인 경우, nums[end]의 값이 2가 아닌 값이면 배열 nums의 idx번째 값과 바꾸고 end 값을 감소시킨다.
- 그 외인 nums[idx]의 값이 1인 경우, idx의 값을 증가시킨다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortColors.java){:target="_blank"}에서 확인 가능합니다.