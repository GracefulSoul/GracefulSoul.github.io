---
title: "Leetcode Java Minimum Size Subarray Sum"
excerpt: "Leetcode Minimum Size Subarray Sum Java 풀이"
last_modified_at: 2021-10-14T09:00:00
header:
  image: /assets/images/leetcode/minimum-size-subarray-sum.png
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
[Link](https://leetcode.com/problems/minimum-size-subarray-sum/){:target="_blank"}

# 코드
```java
class Solution {
  
  public int minSubArrayLen(int target, int[] nums) {
    int length = nums.length;
    int result = length + 1;
    int index = 0;
    for (int i = 0; i < length; i++) {
      target -= nums[i];
      while (target <= 0) {
        result = Math.min(result, i - index + 1);
        target += nums[index++];
      }
    }
    return result % (length + 1);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/570826483/){:target="_blank"}

# 설명
1. 주어진 배열 nums를 이용하여 부분 배열을 만들고 해당 값들의 합이 주어진 정수 target이 되기 위한 최소 배열 크기를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 주어진 배열 nums의 크기를 저장한 변수로 nums.length로 정의한다.
- result는 결과를 구하기 위한 변수로 $length + 1$로 정의한다.
- index는 부분 배열의 마지막 위치를 지정할 인덱스로, 0으로 정의한다.

3. nums를 반복하여 target이 되는 최소 배열 크기를 구한다.
- target에 nums[i]값을 빼준다.
- target이 0 이상이 될 때 까지 아래를 수행한다.
  - result에 부분 배열의 합이 target이 되는 최소 배열의 크기인 result와 $i - index + 1$ 중 작은 값을 넣어준다.
  - target에 nums[index] 값을 더해 이전 값으로 돌려주어 최소 배열의 크기를 다시 계산할 수 있도록 초기화한다.

4. 반복이 완료되면 result에 $length + 1$을 나눈 나머지 값을 주어진 문제의 결과로 반환한다.
- result가 $length + 1$이 되는 경우, 모든 값을 더해도 target이 완성되지 않는 경우이다.
- 위의 경우, result가 초기 값인 $length + 1$이 되므로 0을 반환하기 위한 예외 처리이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumSizeSubarraySum.java){:target="_blank"}에서 확인 가능합니다.