---
title: "Leetcode Java Next Greater Element I"
excerpt: "Leetcode Next Greater Element I Java 풀이"
last_modified_at: 2022-05-17T12:00:00
header:
  image: /assets/images/leetcode/next-greater-element-i.png
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
[Link](https://leetcode.com/problems/next-greater-element-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] nextGreaterElement(int[] nums1, int[] nums2) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int idx = 0; idx < nums2.length; idx++) {
      map.put(nums2[idx], idx);
    }
    for (int idx = 0; idx < nums1.length; idx++) {
      nums1[idx] = this.findNextGreaterElement(nums2, map.get(nums1[idx]));
    }
    return nums1;
  }

  private int findNextGreaterElement(int[] nums2, int index) {
    int num = nums2[index];
    for (int idx = index + 1; idx < nums2.length; idx++) {
      if (nums2[idx] > num) {
        return nums2[idx];
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/701105888/){:target="_blank"}

# 설명
1. nums1 내 각 요소들의 값을 nums2에서 찾아 해당 값의 우측에서 가장 가까우면서 현재 값보다 큰 값을 검색하고, 검색한 값들을 nums1의 순서대로 반환하는 문제이다.
- 단, 요소의 값보다 큰 값이 우측에 존재하지 않는 경우 -1을 해당 자리에 넣는다.

2. nums2 내 각 값의 위치를 저장하기 위한 map을 HashMap으로 초기화하고, nums를 반복하여 값을 key에 위치 값은 value로 넣어준다.

3. nums1의 모든 요소를 반복하여 아래를 수행한다.
- nums1의 idx번째 자리에 4번에서 정의한 findNextGreaterElement(int[] nums2, int index) 메서드를 nums1의 idx번째 값을 map에서 nums2 내 위치 값을 찾은 후 index에 넣어 수행한 결과를 넣어 값을 교환해준다.

4. nums2 배열 내 index번째 값보다 큰 index 이후의 값을 찾는 findNextGreaterElement(int[] nums2, int index) 메서드를 정의한다.
- num에 nums2의 index번째 값을 넣어준다.
- $index + 1$부터 nums2의 길이 미만까지 idx를 증가시키며 탐색을 수행한다.
  - nums2의 idx번째 값이 num보다 큰 경우, nums2의 idx번째 값을 반환한다.
- 반복이 종료되면 num보다 큰 값이 우측에 없으므로, -1을 반환한다.

5. 3번의 반복이 완료되면 문제 풀이대로 변환된 값을 가진 nums1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NextGreaterElementI.java){:target="_blank"}에서 확인 가능합니다.