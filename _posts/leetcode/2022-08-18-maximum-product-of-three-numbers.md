---
title: "Leetcode Java Maximum Product of Three Numbers"
excerpt: "Leetcode Maximum Product of Three Numbers Java"
last_modified_at: 2022-08-18T19:20:00
header:
  image: /assets/images/leetcode/maximum-product-of-three-numbers.png
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
[Link](https://leetcode.com/problems/maximum-product-of-three-numbers/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumProduct(int[] nums) {
    if (nums.length == 3) {
      return nums[0] * nums[1] * nums[2];
    }
    int[] max = new int[] { Integer.MIN_VALUE, Integer.MIN_VALUE, Integer.MIN_VALUE };
    int[] min = new int[] { Integer.MAX_VALUE, Integer.MAX_VALUE };
    for (int idx = 0; idx < nums.length; idx++) {
      if (nums[idx] < min[1]) {
        if (nums[idx] < min[0]) {
          min[1] = min[0];
          min[0] = nums[idx];
        } else {
          min[1] = nums[idx];
        }
      }
      if (nums[idx] > max[0]) {
        if (nums[idx] > max[2]) {
          max[0] = max[1];
          max[1] = max[2];
          max[2] = nums[idx];
        } else if (nums[idx] > max[1]) {
          max[0] = max[1];
          max[1] = nums[idx];
        } else {
          max[0] = nums[idx];
        }
      }
    }
    return Math.max(max[2] * max[1] * max[0], max[2] * min[0] * min[1]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/772280399/){:target="_blank"}

# 설명
1. nums 내 세 숫자의 곱이 최댓값되는 값을 구하는 문제이다.

2. nums의 길이가 3인 경우, 세 값의 곱이 최대인 수는 해당 세 숫자의 곱이므로 모든 값을 곱한 값을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- max는 가장 큰 세 값을 저장할 배열로, 정수의 가장 작은 값을 세 개를 넣어 초기화한다.
- min은 가장 작은 두 값을 저장할 배열로, 정수의 가장 큰 값을 두 개 넣어 초기화한다.

4. 0부터 nums의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- nums의 idx 값을 이용하여 가장 작은 두 값을 min에 오름차순으로 넣어준다.
- nums의 idx 값을 이용하여 가장 큰 세 값을 max에 오름차순으로 넣어준다.

5. max의 세 값의 곱과 min의 두 값의 곱과 max의 가장 큰 값의 곱 중 가장 큰 값을 주어진 문제의 결과로 반환한다.
- 가장 큰 세 숫자가 모두 양수인 경우, 앞의 숫자들의 곱은 일반적으로 가장 큰 값이 된다.
- 하지만 음수를 포함하는 경우, 두 값이 모두 음수인 가장 작은 두 값과 한 값이 양수인 가장 큰 값의 곱이 가장 큰 값이 되기도 한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumProductOfThreeNumbers.java){:target="_blank"}에서 확인 가능합니다.