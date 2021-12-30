---
title: "Leetcode Java Create Maximum Number"
excerpt: "Leetcode Create Maximum Number Java 풀이"
last_modified_at: 2021-12-30T16:00:00
header:
  image: /assets/images/leetcode/create-maximum-number.png
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
[Link](https://leetcode.com/problems/create-maximum-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] maxNumber(int[] nums1, int[] nums2, int k) {
    int[] result = new int[k];
    for (int i = Math.max(0, k - nums2.length); i <= Math.min(nums1.length, k); i++) {
      int[] maxNums1 = this.findMax(nums1, i);
      int[] maxNums2 = this.findMax(nums2, k - i);
      int[] merge = this.merge(maxNums1, maxNums2);
      if (this.isGreater(merge, result, 0, 0)) {
        result = merge;
      }
    }
    return result;
  }

  private boolean isGreater(int[] nums1, int[] nums2, int i, int j) {
    while (i < nums1.length && j < nums2.length) {
      if (nums1[i] > nums2[j]) {
        return true;
      } else if (nums1[i] < nums2[j]) {
        return false;
      } else {
        i++;
        j++;
      }
    }
    return i < nums1.length;
  }

  private int[] merge(int[] nums1, int[] nums2) {
    int i = 0;
    int j = 0;
    int length = nums1.length + nums2.length;
    int[] result = new int[length];
    for (int k = 0; k < length; k++) {
      if (this.isGreater(nums1, nums2, i, j)) {
        result[k] = nums1[i++];
      } else {
        result[k] = nums2[j++];
      }
    }
    return result;
  }

  private int[] findMax(int[] nums, int k) {
    int j = 0;
    int length = nums.length;
    int[] result = new int[k];
    for (int i = 0; i < length; i++) {
      while (j > 0 && result[j - 1] < nums[i] && j + length - i > k) {
        j--;
      }
      if (j < k) {
        result[j++] = nums[i];
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/609637188/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums1과 nums2를 이용하여 아래의 조건을 만족하는 k 크기의 최대 값을 가진 배열을 만드는 문제이다.
- 주어진 정수 k는 nums1과 nums2의 길이보다 같거나 작은 숫자로 주어진다.
- nums1과 nums2의 각 배열의 상대적 순서를 유지하여 k 크기의 배열에 크기순으로 넣은 배열이 가장 큰 경우의 배열을 찾아 주어진 문제의 결과로 반환한다.

2. 결과를 넣을 result 배열을 k크기로 초기화한다.

3. 0과 $k - nums2.length$의 값중 큰 값부터 nums1.length와 k 중 작은 값 까지 반복하여 result에 문제의 결과를 넣어준다.

4. maxNums1에 nums1의 값들 중 가장 큰 값을 포함한 일련된 i개의 숫자로 배열을 만들어 넣어주고, maxNums2에 nums2의 값들 중 가장 큰 값을 포함한 일련된 $k - i$개의 숫자로 배열을 만들어 넣어준다.
- findMax(int[] nums, int k) 메서드는 nums의 숫자들을 모두 순회하여 일련된 가장 큰 값을 포함한 k개의 숫자로 배열을 만들어 넣어준다.

5. 4번을 통해 큰 값들을 찾은 두 배열인 maxNums1과 maxNums2를 숫자 크기의 내림차순으로 합친 배열을 merge에 넣어준다.
- merge(int[] nums1, int[] nums2) 메서드는 nums1과 nums2의 값들이 들어갈 크기의 배열을 선언하여 어느 값이 큰지를 isGreater(int[] nums1, int[] nums2, int i, int j) 메서드를 이용하여 검증하여 해당 배열에 넣어주고, 해당 배열을 반환한다.

6. isGreater(int[] nums1, int[] nums2, int i, int j) 메서드를 이용하여 merge와 result를 처음 값부터 비교하여 어느 배열이 순차적으로 큰 값으로 존재하는지를 검증하고, merge가 큰 경우 result에 넣고 반복을 계속 수행한다.

7. 반복이 완료되면 nums1과 nums2의 각 배열의 상대적 순서를 유지하여 k 크기의 배열에 크기순으로 넣은 배열이 가장 큰 경우의 배열인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CreateMaximumNumber.java){:target="_blank"}에서 확인 가능합니다.