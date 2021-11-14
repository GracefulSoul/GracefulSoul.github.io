---
title: "Leetcode Java Product of Array Except Self"
excerpt: "Leetcode Product of Array Except Self Java 풀이"
last_modified_at: 2021-11-14T12:00:00
header:
  image: /assets/images/leetcode/product-of-array-except-self.png
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
[Link](https://leetcode.com/problems/product-of-array-except-self/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] productExceptSelf(int[] nums) {
    int length = nums.length;
    int[] result = new int[length];
    result[0] = 1;
    for (int idx = 1; idx < length; idx++) {
      result[idx] = result[idx - 1] * nums[idx - 1];
    }
    int right = 1;
    for (int idx = length - 1; idx >= 0; idx--) {
      result[idx] *= right;
      right *= nums[idx];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/586786954/){:target="_blank"}

# 설명
1. 

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ProductOfArrayExceptSelf.java){:target="_blank"}에서 확인 가능합니다.