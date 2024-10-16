---
title: "Leetcode Java Maximum Product Subarray"
excerpt: "Leetcode Maximum Product Subarray Java 풀이"
last_modified_at: 2021-09-09T12:00:00
header:
  image: /assets/images/leetcode/maximum-product-subarray.png
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
[Link](https://leetcode.com/problems/maximum-product-subarray/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxProduct(int[] nums) {
    int max = nums[0];
    int length = nums.length;
    int left = 1;
    int right = 1;
    for (int idx = 0; idx < length; idx++) {
      left = (left == 0 ? 1 : left) * nums[idx];
      right = (right == 0 ? 1 : right) * nums[length - 1 - idx];
      max = Math.max(max, Math.max(left, right));
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/551796642/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums의 부분 집합의 곱이 최대인 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 부분 집합의 곱이 최대인 값을 저장하기 위한 변수이다.
- length는 nums의 길이를 저장하는 변수이다.
- left는 left-right로 이동하며 곱한 값을 저장하기 위한 변수이다.
- right는 right-left로 이동하며 곱한 값을 저장하기 위한 변수이다.

3. 배열 nums를 반복하여 부분 집합의 곱이 최대인 값을 구한다.
- left가 0인 경우 1과, 그렇지 않은 경우 left와 nums[idx]값의 곱을 다시 left에 넣어준다.
- right가 0인 경우 1과, 그렇지 않은 경우 left와 nums[$length - 1 - idx$]값의 곱을 다시 right에 넣어준다.
  - 각 left와 right가 0인 경우 nums[$idx - 1$]값 혹은 nums[$length - 1 - idx - 1$]값이 0이어서 곱의 결과가 0으로 저장된 경우이므로, 다음 계산을 위해 1로 변환하는 것이다.
- max를 left, right, max 중 가장 큰 값으로 넣어준다.

4. 반복이 종료되면 부분 집합의 곱이 최대인 값을 저장한 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumProductSubarray.java){:target="_blank"}에서 확인 가능합니다.