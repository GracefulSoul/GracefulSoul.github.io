---
title: "Leetcode Java Search in Rotated Sorted Array"
excerpt: "Leetcode - 'Search in Rotated Sorted Array' 문제 Java 풀이"
last_modified_at: 2021-05-16T17:10:00
header:
  image: /assets/images/leetcode/search-in-rotated-sorted-array.png
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
[Link](https://leetcode.com/problems/search-in-rotated-sorted-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int search(int[] nums, int target) {
    for (int idx = 0; idx < nums.length; idx++) {
      if (nums[idx] == target) {
        return idx;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/493873852/){:target="_blank"}

# 설명
1. 주어진 문제는 어렵게 생각할 필요 없이, 배열 내 주어진 target의 index를 반환하는 문제이다.

2. 반복문을 통해 해당 값을 찾아서 index를 주어진 문제의 결과로 반환하면 된다.

3. 단, 배열 내 target의 값이 존재하지 않을 경우, -1을 주어진 문제의 결과로 반환하면 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SearchInRotatedSortedArray.java){:target="_blank"}에서 확인 가능합니다.