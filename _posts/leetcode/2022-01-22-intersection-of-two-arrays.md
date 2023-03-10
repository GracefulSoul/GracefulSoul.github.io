---
title: "Leetcode Java Intersection of Two Arrays"
excerpt: "Leetcode Intersection of Two Arrays Java 풀이"
last_modified_at: 2022-01-22T09:00:00
header:
  image: /assets/images/leetcode/intersection-of-two-arrays.png
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
[Link](https://leetcode.com/problems/intersection-of-two-arrays/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] intersection(int[] nums1, int[] nums2) {
    int[] count = new int[1000];
    for (int num : nums1) {
      count[num]++;
    }
    int[] result = new int[nums1.length];
    int index = 0;
    for (int num : nums2) {
      if (count[num] > 0) {
        result[index++] = num;
        count[num] = 0;
      }
    }
    return Arrays.copyOf(result, index);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/624904682/){:target="_blank"}

# 설명
1. 주어진 정수 배열인 nums1과 nums2 내 동일하게 들어있는 값들을 중복 제거하여 반환하는 문제이다.

2. 숫자의 개수를 저장할 배열인 count를 주어진 배열 내 정수가 가질 수 있는 최대값인 1000 크기로 정의하고, nums1을 순회하여 count의 내부 값들의 개수를 증가시켜준다.

3. 결과를 담을 result 배열을 nums1의 크기로, 해당 배열에 값을 순차적으로 넣기 위한 index를 0으로 정의한다.
- result의 크기를 nums1 크기로 정의한 이유는, 주어진 두 배열인 nums1과 nums2 내 중복된 값의 개수는 두 배열 중 가장 작은 크기의 배열 크기 이하로만 존재할 수 있다.
- 임의 배열 크기로 정의하고 index까지 배열을 자를 예정이므로 둘 중 아무 크기로 정의해도 상관없다.

4. nums2를 반복하여 count의 num번째 값이 0 초과(nums1에 존재하는 값)인 경우, result에 num을 넣고 index를 증가시키고 count의 num번째 값을 0으로 초기화 시킨다.

5. 반복이 완료되면 nums1과 nums2의 중복된 값을 넣은 result 배열의 index개 값들로 신규 배열에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IntersectionOfTwoArrays.java){:target="_blank"}에서 확인 가능합니다.