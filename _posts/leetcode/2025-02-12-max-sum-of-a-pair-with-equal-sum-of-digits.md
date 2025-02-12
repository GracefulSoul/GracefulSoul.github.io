---
title: "Leetcode Java Max Sum of a Pair With Equal Sum of Digits"
excerpt: "Leetcode - 'Max Sum of a Pair With Equal Sum of Digits' 문제 Java 풀이"
last_modified_at: 2025-02-12T17:50:00
header:
  image: /assets/images/leetcode/max-sum-of-a-pair-with-equal-sum-of-digits.png
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
[Link](https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumSum(int[] nums) {
    int[] max = new int[82];
    int result = -1;
    for (int num : nums) {
      int sum = 0;
      int temp = num;
      while (temp != 0) {
        sum += temp % 10;
        temp /= 10;
      }
      if (max[sum] != 0) {
        result = Math.max(result, num + max[sum]);
      }
      max[sum] = Math.max(max[sum], num);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/max-sum-of-a-pair-with-equal-sum-of-digits/submissions/1540280906/){:target="_blank"}

# 설명
1. 양의 정수로 구성된 nums 내 아래 규칙을 만족하는 최댓값 $nums[i] + nums[j]$를 구하는 문제이다.
- 서로 다른 임의 위치 i와 j를 고르되, nums[i] 값과 nums[j] 값의 값 각 자리 별 숫자의 합은 동일하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 최댓값을 저장할 변수로, 각 숫자별 합계가 최대가 될 수 있는 상한값인 82 크기의 정수 배열로 초기화한다.
- result는 결과를 저장할 변수로, -1로 초기화한다.

3. nums의 각 값을 num에 넣어 순차적으로 아래를 수행한다.
- sum은 합계를 저장할 변수로, 0으로 초기화하고 num을 temp에 넣어 각 자리 별 숫자의 합계를 더해준다.
- max[sum]의 값이 0이 아닌 경우 이전에 계산한 값이 존재하므로, result에 result와 $num + max[sum]$ 중 합계가 큰 값을 넣어준다.
- max[sum]에 max[sum] 값과 num 중 큰 값을 넣어 저장한다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxSumOfAPairWithEqualSumOfDigits.java){:target="_blank"}에서 확인 가능합니다.