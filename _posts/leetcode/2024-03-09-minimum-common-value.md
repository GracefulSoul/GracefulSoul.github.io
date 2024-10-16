---
title: "Leetcode Java Minimum Common Value"
excerpt: "Leetcode Minimum Common Value Java"
last_modified_at: 2024-03-09T10:00:00
header:
  image: /assets/images/leetcode/minimum-common-value.png
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
[Link](https://leetcode.com/problems/minimum-common-value){:target="_blank"}

# 코드
```java
class Solution {

  public int getCommon(int[] nums1, int[] nums2) {
    for (int i = 0, j = 0; i < nums1.length && j < nums2.length;) {
      if (nums1[i] == nums2[j]) {
        return nums1[i];
      } else if (nums1[i] < nums2[j]) {
        i++;
      } else {
        j++;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-common-value/submissions/1198052970/){:target="_blank"}

# 설명
1. 오름차순으로 정렬된 nums1과 nums2 배열에 공통적으로 존재하는 값들 중 가장 작은 값을 반환하는 문제이다.
- 단, 공통적으로 존재하는 값이 없는 경우 -1을 주어진 문제의 결과로 반환한다.

2. i와 j를 0으로 초기화하여 nums1과 nums2의 길이 미만일 때까지 아래를 반복한다.
- nums1[i]의 값이 nums2[j]의 값과 동일한 경우, 해당 값을 주어진 문제의 결과로 반환한다.
- nums1[i]의 값이 nums2[j]의 값보다 작은 경우, i를 증가시키고 그 반대의 경우 j를 증가시킨다.

3. 반복이 완료되면 공통적으로 존재하는 값이 없다는 의미이므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumCommonValue.java){:target="_blank"}에서 확인 가능합니다.