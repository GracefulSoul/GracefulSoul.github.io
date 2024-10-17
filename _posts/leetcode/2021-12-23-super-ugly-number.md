---
title: "Leetcode Java Super Ugly Number"
excerpt: "Leetcode - 'Super Ugly Number' 문제 Java 풀이"
last_modified_at: 2021-12-23T13:00:00
header:
  image: /assets/images/leetcode/super-ugly-number.png
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
[Link](https://leetcode.com/problems/super-ugly-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int nthSuperUglyNumber(int n, int[] primes) {
    int[] nums = new int[n];
    int pre = 1;
    int min = 1;
    int length = primes.length;
    int[] idx = new int[length];
    int[] prePrimes = new int[length];
    Arrays.fill(prePrimes, 1);
    for (int i = 0; i < n; i++) {
      nums[i] = min;
      min = Integer.MAX_VALUE;
      for (int j = 0; j < length; j++) {
        if (prePrimes[j] == pre) {
          prePrimes[j] = primes[j] * nums[idx[j]];
          idx[j]++;
        }
        min = Math.min(prePrimes[j], min);
      }
      pre = min;
    }
    return nums[n - 1];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/605792815/){:target="_blank"}

# 설명
1. 주어진 정수 배열 primes의 소인수를 이용한 숫자를 만들 때 n번째가 되는 정수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 primes의 소인수를 이용한 숫자를 넣을 배열로, 주어진 정수 n의 크기로 초기화한다.
- pre는 이전의 값을 저장하는 변수이다.
- min은 pre 다음에 나올 primes의 소인수를 이용한 숫자를 저장할 변수이다.
- length는 primes의 길이를 저장할 변수이다.
- idx는 primes의 동일 위치의 값을 반복한 횟수를 저장할 배열로, length의 크기로 초기화한다.
- prePrimes는 primes를 이용하여 idx의 동일 위치번쨰 반복한 결과를 넣을 배열로, length의 크기로 초기화하고 모든 위치의 값을 1로 초기화한다.

3. 0부터 n 전까지 i를 증가시키면서 반복하여 nums에 값을 넣어준다.
- nums의 i번째 위치에 min 값을 넣어준다.
- min 값에 Integer의 가장 큰 값을 넣어준다.
- 0부터 length 전까지 j를 증가시키면서 반복하여 min 값을 구한다.
  - prePrimes의 j번쨰 값이 pre와 동일한 경우, prePrimes[j]의 값에 $primes[j] \times num[idx[j]]$ 결과를 넣어주고 j를 증가시킨다.
  - min과 prePrimes[j]의 최소 값을 min에 넣어준다.
- pre에 min 값을 넣어준다.

4. primes의 소인수를 이용한 숫자를 만들 때 n번째 값이 되는 nums의 $n - 1$번째 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SuperUglyNumber.java){:target="_blank"}에서 확인 가능합니다.