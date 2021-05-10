---
title: "Leetcode Java Remove Duplicates from Sorted Array"
excerpt: "Leetcode Remove Duplicates from Sorted Array Java 풀이"
last_modified_at: 2021-05-10T21:10:00
header:
  image: /assets/images/leetcode/remove-element.png
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
[Link](https://leetcode.com/problems/remove-element/){:target="_blank"}

# 코드
```java
class Solution {

  public int removeElement(int[] nums, int val) {
    int i = 0;
    for (int n : nums) {
      if (n != val) {
        nums[i++] = n;
      }
    }
    return i;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/491277685/){:target="_blank"}

# 설명
1. 주어진 배열 nums을 반복으로 주어진 정수 val과 다른 값의 갯수를 파악한다.
  - 주어진 배열 nums의 내부 값이 val과 다르다면 i의 값을 점층적으로 증가시킨다.

2. 반복이 종료되면 주어진 정수 val과 다른 값의 갯수를 저장한 i의 값을 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveElement.java){:target="_blank"}에서 확인 가능합니다.