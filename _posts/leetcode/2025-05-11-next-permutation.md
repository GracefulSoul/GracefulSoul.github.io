---
title: "Leetcode Java Next Permutation"
excerpt: "Leetcode - 'Next Permutation' 문제 Java 풀이"
last_modified_at: 2025-05-11T19:10:00
header:
  image: /assets/images/leetcode/next-permutation.png
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
[Link](https://leetcode.com/problems/next-permutation/){:target="_blank"}

# 코드
```java
class Solution {

  public void nextPermutation(int[] nums) {
    int length = nums.length;
    if (1 < length) {
      int i = length - 2;
      while (0 <= i && nums[i + 1] <= nums[i]) {
        i--;
      }
      if (0 <= i) {
        int j = length - 1;
        while (nums[j] <= nums[i]) {
          j--;
        }
        this.swap(nums, i, j);
      }
      this.reverse(nums, i + 1, length - 1);
    }
  }

  private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
  }

  private void reverse(int[] nums, int i, int j) {
    while (i < j) {
      this.swap(nums, i++, j--);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/next-permutation/submissions/1630936351/){:target="_blank"}

# 설명
1. nums의 사전적으로 다음에 올 수 있는 순열로 변환하는 문제이다.
- 단, 현재 배열이 사전적으로 다음에 올 수 있는 순열이 없으면 사전적으로 가장 작은 순열로 변환한다.

2. length는 nums의 길이를 저장한 변수로, 1 초과인 경우만 변환 가능하므로 다음을 수행한다.
- i는 시작 지점을 탐색할 위치를 저장할 변수로, $length - 2$로 초기화하고 i가 처음 위치일 때까지 사전적으로 작은 위치를 탐색하여 넣어준다.
- i가 0보다 큰 경우, 아래를 반복한다.
  - j인 마지막 지점을 탐색할 위치를 저장할 변수로, $length - 1$로 넣어 nums[j]의 값이 nums[i]의 값보다 작거나 같을 때 까지 j를 감소시켜준 후 nums 내 i번째 값과 j번째 값을 바꿔준다.
- nums의 $i + 1$번째 값과 $length - 1$번째 값을 역순으로 치환하여 순서를 다시 정렬해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NextPermutation.java){:target="_blank"}에서 확인 가능합니다.