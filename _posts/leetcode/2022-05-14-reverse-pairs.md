---
title: "Leetcode Java Reverse Pairs"
excerpt: "Leetcode - 'Reverse Pairs' 문제 Java 풀이"
last_modified_at: 2022-05-14T16:00:00
header:
  image: /assets/images/leetcode/reverse-pairs.png
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
[Link](https://leetcode.com/problems/reverse-pairs/){:target="_blank"}

# 코드
```java
class Solution {

  public int reversePairs(int[] nums) {
    return this.mergeSort(nums, 0, nums.length - 1);
  }

  private int mergeSort(int[] nums, int start, int end) {
    if (start >= end) {
      return 0;
    }
    int mid = (start + end) / 2;
    int result = this.mergeSort(nums, start, mid) + this.mergeSort(nums, mid + 1, end);
    for (int i = start, j = mid + 1; i <= mid; i++) {
      while (j <= end && nums[i] / 2.0 > nums[j]) {
        j++;
      }
      result += j - (mid + 1);
    }
    Arrays.sort(nums, start, end + 1);
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/699122971/){:target="_blank"}

# 설명
1. nums 내 아래의 조건을 만족하는 역방향 숫자 쌍의 수를 반환하는 문제이다.
- 역 방향 쌍인 [i, j]는 $0 <= i < j < nums.length$을 만족한다.
- 역 방향 쌍인 [i, j]는 $nums[i] > 2 \times nums[j]$을 만족한다.

2. 3번에서 정의한 mergeSort(int[] nums, int start, int end) 메서드에 start는 0, end는 nums의 길이보다 1 작게 수행한 결과를 주어진 문제의 결과로 반환한다.

3. 병합 정렬을 이용해 역방향 숫자 쌍의 수를 계산할 mergeSort(int[] nums, int start, int end) 메서드를 정의한다.
- start가 end에 도달한 경우 정렬할 숫자가 없으므로, 0을 반환한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - mid는 start와 end의 중간 값을 넣기 위한 변수로, $\frac{start + end}{2}$의 결과를 넣어준다.
  - result는 병합 정렬에 수행된 숫자의 개수를 넣을 변수로, mid를 end에 넣어 재귀 호출을 수행한 결과와 $mid + 1$을 start에 넣어 재귀 호출을 수행한 결과의 합을 넣어 초기화한다.
- start부터 mid까지 i를 증가시키고, j는 $mid + 1$로 초기화 하여 반복을 수행한다.
  - 주어진 조건인 j가 end 이하이고 nums의 i번째 값을 2.0으로 나눈 값이 nums의 j번째 값보다 큰 경우, j를 증가시켜 j의 위치를 증가시킨다. (위의 조건 중 $nums[i] > 2 \times nums[j]$는 overflow가 발생 가능하므로, $\frac{nums[i]}{2} > nums[j]$로 로직을 변경해서 수행한다.)
  - j에 $mid + 1$의 값을 뺀 결과인 이동 횟수를 넣어준다.
- nums를 start 위치부터 $end + 1$ 위치까지 정렬하고, 정렬이 수행된 숫자의 개수인 result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReversePairs.java){:target="_blank"}에서 확인 가능합니다.