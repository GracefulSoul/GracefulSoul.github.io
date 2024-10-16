---
title: "Leetcode Java Number of Subarrays with Bounded Maximum"
excerpt: "Leetcode Number of Subarrays with Bounded Maximum Java"
last_modified_at: 2023-01-07T09:15:00
header:
  image: /assets/images/leetcode/number-of-subarrays-with-bounded-maximum.png
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
[Link](https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum){:target="_blank"}

# 코드
```java
class Solution {

  public int numSubarrayBoundedMax(int[] nums, int left, int right) {
    return this.getCount(nums, right) - this.getCount(nums, left - 1);
  }

  private int getCount(int[] nums, int bound) {
    int total = 0;
    int count = 0;
    for (int num : nums) {
      count = num <= bound ? count + 1 : 0;
      total += count;
    }
    return total;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/valid-tic-tac-toe-state/submissions/871904979/){:target="_blank"}

# 설명
1. nums 내 값을 이용하여 [left, right] 범위에 존재하는 연속된 숫자들을 이용한 부분 배열의 수를 구하는 문제이다.

2. nums 내 bound까지 부분 배열의 수를 계산할 getCount(int[] nums, int bound) 메서드를 정의한다.
- 부분 배열의 수를 계산할 변수를 정의한다.
  - total은 bound까지 부분 배열의 총 개수를 저장할 변수로, 0으로 초기화한다.
  - count는 nums 내 연속된 값들을 이용한 부분 배열의 숫자를 저장할 변수로, 0으로 초기화한다.
- nums의 값들을 차례대로 num에 넣어 아래를 수행한다.
  - num이 bound 이하인 경우 count를 증가시키고, 초과인 경우 범위를 넘었으므로 count를 0으로 초기화한다.
  - total에 num 위치까지 부분 배열의 수를 저장한 count를 더해준다.
- 반복이 완료되면 bound까지 부분 배열의 수를 저장한 total을 반환한다.

3. 2번에서 정의한 getCount(int[] nums, int bound) 메서드를 이용하여 right까지 범위의 부분 배열의 수에 left까지 범위의 부분 배열의 수를 뺀 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfSubarraysWithBoundedMaximum.java){:target="_blank"}에서 확인 가능합니다.