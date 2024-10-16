---
title: "Leetcode Java First Missing Positive"
excerpt: "Leetcode First Missing Positive Java 풀이"
last_modified_at: 2021-05-22T11:40:00
header:
  image: /assets/images/leetcode/first-missing-positive.png
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
[Link](https://leetcode.com/problems/first-missing-positive/){:target="_blank"}

# 코드
```java
class Solution {

  public int firstMissingPositive(int[] nums) {
    int idx = 0;
    while (idx < nums.length) {
      if (nums[idx] >= 1 && nums[idx] <= nums.length && nums[idx] > nums[nums[idx] - 1]) {
        this.swap(nums, idx, nums[idx] - 1);
      } else {
        idx++;
      }
    }
    idx = 0;
    while (idx < nums.length && nums[idx] == idx + 1) {
      idx++;
    }
    return idx + 1;
  }

  private void swap(int[] nums, int left, int right) {
    int temp = nums[left];
    nums[left] = nums[right];
    nums[right] = temp;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/496468825/){:target="_blank"}

# 설명
1. 주어진 배열 nums에 포함되지 않은 가능한 최소의 양의 정수 값을 구하는 문제이다.

2. 주어진 배열 nums를 반복하기 위해 idx를 0으로 초기화 하고, 반복문을 통해 배열 내 값들을 정렬한다.
- 아래의 조건을 만족 하는 경우, 정렬을 하고 그렇지 않은 경우 idx 값을 증가시킨다.
  - nums[idx] 값이 1보다 크거나 같다(양의 정수이다).
  - nums.length 값보다 작거나 같다(정렬된 양의 정수이다).
  - nums[idx] != nums[nums[idx] - 1]과 다르다(idx의 값이 idx번째 값인지를 검증한다).

3. 배열 내 값들이 정렬되면 idx 값을 0으로 다시 초기화 시키고 가능한 최소한의 양의 정수를 반복문을 통해 구한다.
- 만일 nums.length만큼 반복하되, nums[idx]가 1부터 시작하는 양의 정수로 정렬되는 경우 idx를 증가시킨다.
- 위의 경우가 아닌 경우, 반복문이 종료된다.

4. 반복문이 종료되면, 정렬된 양의 정수의 index인 idx에 1을 추가하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FirstMissingPositive.java){:target="_blank"}에서 확인 가능합니다.