---
title: "Leetcode Java Subarray Sums Divisible by K"
excerpt: "Leetcode Subarray Sums Divisible by K Java"
last_modified_at: 2023-08-14T20:30:00
header:
  image: /assets/images/leetcode/subarray-sums-divisible-by-k.png
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
[Link](https://leetcode.com/problems/subarray-sums-divisible-by-k){:target="_blank"}

# 코드
```java
class Solution {

  public int subarraysDivByK(int[] nums, int k) {
    int result = 0;
    int prefix = 0;
    int[] count = new int[k];
    count[0] = 1;
    for (int num : nums) {
      prefix = (prefix + (num % k) + k) % k;
      result += count[prefix];
      count[prefix]++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/subarray-sums-divisible-by-k/submissions/1021055416/){:target="_blank"}

# 설명
1. 연속된 값이 k의 배수가 되는 부분 배열의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 부분 배열의 수를 계산할 변수로, 0으로 초기화한다.
- prefix는 값들을 더한 후 k로 나눈 나머지를 저장할 변수로, 0으로 초기화한다.
- count는 k로 나눈 나머지 값의 갯수를 저장할 변수로, k 크기의 정수 배열로 초기화하고 첫 값에 1을 넣어준다.

3. nums의 모든 값을 순차적으로 num에 넣어 아래를 반복한다.
- prefix에 prefix와 num을 k로 나눈 나머지 값과 더한 후 k로 나눈 나머지 값을 넣어준다.
- result에 count의 prefix번째 값에 대한 갯수를 꺼내 더해주고, count의 prefix번째 값을 증가시킨다.

4. 반복이 완료되면 부분 배열의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SubarraySumsDivisibleByK.java){:target="_blank"}에서 확인 가능합니다.