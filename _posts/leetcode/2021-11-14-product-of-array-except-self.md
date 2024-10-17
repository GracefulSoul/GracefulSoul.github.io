---
title: "Leetcode Java Product of Array Except Self"
excerpt: "Leetcode - 'Product of Array Except Self' 문제 Java 풀이"
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
1. 주어진 nums를 이용하여 동일한 위치 값의 곱셈 결과가 모든 요소를 곱한 값과 동일한 배열을 만드는 문제이다.
- O(n)의 시간 복잡도를 가지는 알고리즘을 작성해야 한다.
- 나눗셈 연산자를 사용하지 말아야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장하여 활용하기 위한 변수이다.
- result는 nums의 같은 위치의 값의 곱이 모든 요소를 곱한 값과 동일한 값을 만들기 위한 배열로, 첫 값인 result[0]에 1을 넣어준다.

3. result의 두 번째 위치부터 반복하여 result[idx] 값을 넣어준다.
- result[idx]에 result[$idx - 1$]의 값과 nums[$idx - 1$]의 값의 곱을 넣어준다.

4. 우측에서부터 result에 결과를 채우기 위해 반복하여 아래를 수행한다.
- result[idx]에 right와 곱한 값을 넣어준다.
- right에 nums[idx]의 값과 곱한 값을 넣어준다.

5. 반복이 완료되어 result가 채워지면 result를 주어진 문제의 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ProductOfArrayExceptSelf.java){:target="_blank"}에서 확인 가능합니다.