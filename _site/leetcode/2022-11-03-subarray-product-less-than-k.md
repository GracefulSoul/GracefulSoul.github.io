---
title: "Leetcode Java Subarray Product Less Than K"
excerpt: "Leetcode Subarray Product Less Than K Java"
last_modified_at: 2022-11-03T18:50:00
header:
  image: /assets/images/leetcode/subarray-product-less-than-k.png
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
[Link](https://leetcode.com/problems/subarray-product-less-than-k){:target="_blank"}

# 코드
```java
class Solution {

  public int numSubarrayProductLessThanK(int[] nums, int k) {
    if (k == 0) {
      return 0;
    }
    int count = 0;
    int product = 1;
    for (int i = 0, j = 0; j < nums.length; j++) {
      product *= nums[j];
      while (i <= j && product >= k) {
        product /= nums[i++];
      }
      count += j - i + 1;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/835974832/){:target="_blank"}

# 설명
1. num의 연속된 값들의 부분 배열 내 모든 값을 곱한 결과가 k 미만인 부분 배열의 수를 구하는 문제이다.

2. nums내 최솟값은 1로 k가 0인 경우 나올 수 있는 경우가 없으므로, 0을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- count는 부분 배열 내 곱의 결과가 k 미만인 부분 배열의 수를 저장할 변수로, 0으로 초기화한다.
- product는 부분 배열 내 곱의 결과를 저장할 변수로, 최소 크기인 1로 초기화한다.

4. i를 0으로 초기화시키고, 0부터 nums의 길이 미만까지 j를 증가시키며 아래를 반복한다.
- product에 nums의 j번째 값을 곱해준다.
- i가 j 이하이고 product가 k 이상일 때까지 아래를 반복하여 부분 배열을 만들 수 있는 개수를 산정한다.
  - product에 nums의 i번째 값을 나누어 k 미만이 되는 부분 배열 곱의 결과를 구한다.
  - i를 증가시킨 후 반복을 계속 수행하여 부분 배열에 포함될 숫자의 범위를 좁혀준다.
- 위를 통해 좁혀진 범위인 i와 j를 이용하여 $j - i + 1$을 count에 더해준다.

5. 반복이 완료되면 부분 배열의 수를 계산한 count를 주어진 문제의 결과로 반환한다.

# 해설
- nums가 [10, 5, 2, 6]이고, k가 13인 경우를 예를 보면 아래의 두 경우가 복수개의 부분 배열의 범위가 된다.
  - i가 2인 값이 2의 위치인 경우, 10이 포함되면 k를 넘으므로 [5, [2]] 형태로 [2], [5, 2]가 k 미만의 부분 집합이 2개가 된다.
  - i가 3인 값이 6의 위치인 경우, 5부터 포함되면 k를 넘으므로 [2, [6]] 형태로 [6], [2, 6]가 k 미만의 부분 집합이 2개가 된다.
- 위와 같이 특정 값 미만의 연속된 값들이 부분 배열이 되면 해당 숫자 개수만큼 부분 배열이 완성된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SubarrayProductLessThanK.java){:target="_blank"}에서 확인 가능합니다.