---
title: "Leetcode Java Maximum Product of Two Elements in an Array"
excerpt: "Leetcode Maximum Product of Two Elements in an Array Java"
last_modified_at: 2023-12-12T20:20:00
header:
  image: /assets/images/leetcode/maximum-product-of-two-elements-in-an-array.png
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
[Link](https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProduct(int[] nums) {
    int[] max = new int[] { Integer.MIN_VALUE, Integer.MIN_VALUE };
    for (int num : nums) {
      if (num > max[0]) {
        max[1] = max[0];
        max[0] = num;
      } else if (num > max[1]) {
        max[1] = num;
      }
    }
    return (max[0] - 1) * (max[1] - 1);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/submissions/1117986154/){:target="_blank"}

# 설명
1. nums 내 가장 큰 두 값을 이용하여 각 값에서 1을 빼고 곱한 결과를 구하는 문제이다.

2. max는 가장 큰 두 값을 저장하기 위한 변수로, 두 값을 저장해야하므로 2 크기의 정수 배열에 정수의 가장 작은 값을 넣어 초기화한다.

3. nums의 모든 값을 반복하여 max에 가장 큰 두 값을 찾아 넣어준다.

4. 가장 큰 두 값을 이용하여 $(max[0] - 1) \times (max[1] - 1)$를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumProductOfTwoElementsInAnArray.java){:target="_blank"}에서 확인 가능합니다.