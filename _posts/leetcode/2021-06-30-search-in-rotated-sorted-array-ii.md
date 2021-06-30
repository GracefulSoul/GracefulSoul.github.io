---
title: "Leetcode Java Search in Rotated Sorted Array II"
excerpt: "Leetcode Search in Rotated Sorted Array II Java 풀이"
last_modified_at: 2021-06-30T12:40:00
header:
  image: /assets/images/leetcode/search-in-rotated-sorted-array-ii.png
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
[Link](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean search(int[] nums, int target) {
    for (int num : nums) {
      if (num == target) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/515187191/){:target="_blank"}

# 설명
1. 주어진 정렬되지 않은 배열 nums에서 target이 존재하는지 확인하는 문제이다.

2. 반복문을 통해서 num과 target이 동일하면 true를 주어진 문제의 결과로 반환한다.

3. 반복문이 종료되면 배열 nums에 target이 존재하지 않으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SearchInRotatedSortedArrayII.java){:target="_blank"}에서 확인 가능합니다.