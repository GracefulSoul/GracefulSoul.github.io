---
title: "Leetcode Java Merge Sorted Array"
excerpt: "Leetcode Merge Sorted Array Java 풀이"
last_modified_at: 2021-07-07T18:00:00
header:
  image: /assets/images/leetcode/merge-sorted-array.png
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
[Link](https://leetcode.com/problems/merge-sorted-array/){:target="_blank"}

# 코드
```java
class Solution {

  public void merge(int[] nums1, int m, int[] nums2, int n) {
    int length = m + n - 1;
    m--; n--;
    while (n >= 0) {
      nums1[length--] = m < 0 || nums1[m] < nums2[n] ? nums2[n--] : nums1[m--];
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/518593122/){:target="_blank"}

# 설명
1. 주어진 배열 nums1의 m자리 까지의 값들과, 주어진 배열 nums2의 n자리 까지의 값들을 오름차순으로 nums1에 다시 넣어주는 문제이다.

2. 주어진 두 정수 m과 n을 합한 값에서 1을 뺀 값으로 변수 length를 정의한다.

3. 주어진 두 정수 m과 n의 index를 활용하기 위하여 각각 1을 빼준다.

4. 반복문을 통해 nums2의 값을 nums1에 오름차순으로 정렬된 순서로 넣어준다.
- m이 0이 아니거나 nums1[m]이 nums2[n]보다 작을 경우 nums2[n] 값을 nums1[length] 값에 넣어주고, n과 length를 감소시킨다.
- 위의 경우가 아닌 경우 nums1[m]의 값을 nums1[length]에 넣어주고 m과 length를 감소시킨다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MergeSortedArray.java){:target="_blank"}에서 확인 가능합니다.