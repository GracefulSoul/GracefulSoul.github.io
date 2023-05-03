---
title: "Leetcode Java Sort an Array"
excerpt: "Leetcode Sort an Array Java"
last_modified_at: 2023-05-02T19:20:00
header:
  image: /assets/images/leetcode/sort-an-array.png
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
[Link](https://leetcode.com/problems/sort-an-array){:target="_blank"}

# 코드
```java
class Solution {

  public int[] sortArray(int[] nums) {
    this.mergeSort(nums, 0, nums.length - 1);
    return nums;
  }

  private void mergeSort(int[] nums, int left, int right) {
    if (left >= right) {
      return;
    }
    int mid = left + (right - left) / 2;
    this.mergeSort(nums, left, mid);
    this.mergeSort(nums, mid + 1, right);
    int[] temp = new int[right - left + 1];
    int i = left;
    int j = mid + 1;
    int k = 0;
    while (i <= mid || j <= right) {
      if (i > mid || (j <= right && nums[i] > nums[j])) {
        temp[k++] = nums[j++];
      } else {
        temp[k++] = nums[i++];
      }
    }
    System.arraycopy(temp, 0, nums, left, right - left + 1);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sort-an-array/submissions/943161133/){:target="_blank"}

# 설명
1. nums를 내장 함수를 사용하지 않고  O(nlogn) 시간 복잡도로 정렬하는 문제이다.

2. O(nlogn) 시간 복잡도를 사용하는 [병합 정렬](https://en.wikipedia.org/wiki/Merge_sort){:target="_blank"}을 수행하는 mergeSort(int[] nums, int left, int right) 메서드를 정의한다.
- left가 right와 같거나 큰 경우, 수행을 그만한다.
- mid에 $left + \frac{right - left}{2}$를 넣어준다.
- left와 mid 범위로 재귀 호출을 수행한 후, $mid + 1$과 right 범위로 다시 재귀 호출을 수행한다.
- temp는 정렬에 사용할 변수로, $right - left + 1$ 크기의 정수 배열로 초기화한다.
- 정렬에 필요한 변수를 정의한다.
  - i는 [left, mid] 범위의 값을 정렬할 변수로, 첫 위치인 left로 초기화한다.
  - j는 [$mid + 1$, right] 범위의 값을 정렬할 변수로, 첫 위치인 $mid + 1$로 초기화한다.
  - k는 temp의 위치 변수로, 0으로 초기화한다.
- i가 mid 이하이거나 j가 right 이하일 때 까지 아래를 반복한다.
  - i가 mid보다 크거나 j가 right 이하이고 nums의 i번째 값이 j번째 값보다 큰 경우, temp의 k번째 위치에 더 작은 nums의 j번째 값을 넣어주고 j와 k를 증가시켜 다음 위치로 이동시킨다.
  - 위의 경우가 아니라면 temp의 k번째 위치에 nums의 i번째 값을 넣어주고, i와 k를 증가시킨다.
- 반복이 완료되면 nums의 left번째 위치부터 차례대로 temp의 첫 번째 값부터 $right - left + 1$번째 위치의 값까지 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortAnArray.java){:target="_blank"}에서 확인 가능합니다.