---
title: "Codility Java CountSemiprimes"
excerpt: "Lesson11. Sieve Of Eratosthenes"
last_modified_at: 2021-03-01T21:54:00
header:
  image: /assets/images/codility/lesson11/CountSemiprimes.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Sieve Of Eratosthenes
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/11-sieve_of_eratosthenes/count_semiprimes/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int[] solution(int N, int[] P, int[] Q) {
    int[] result = new int[P.length];
    int[] preSum = getPreSum(N);
    for (int idx = 0; idx < P.length; idx++) {
      result[idx] = preSum[Q[idx]] - preSum[P[idx] - 1];
    }
    return result;
  }

  private int[] getPreSum(int N) {
    int[] preSum = new int[N + 1];
    int[] flags = getCheckNumbers(N);
    int semiPrimeCount = 0;
    for (int idx = 2; idx <= N; idx++) {
      if (flags[idx] == 2) {
        semiPrimeCount++;
      }
      preSum[idx] = semiPrimeCount;
    }
    return preSum;
  }

  // 1: No prime, 2: SemiPrime
  private int[] getCheckNumbers(int N) {
    int[] flags = new int[N + 1];
    flags[0] = 1;
    flags[1] = 1;
    for (int idx = 2; idx * idx <= N; idx++) {
      if (flags[idx] == 1) {
        continue;
      }
      int multiple = idx * idx;
      while (multiple <= N) {
        if (flags[idx] == 0 && flags[multiple / idx] == 0) {
          flags[multiple] = 2;
        } else {
          flags[multiple] = 1;
        }
        multiple = multiple + idx; // Next multiple number.
      }
    }
    return flags;
  }
}
```

# 설명
1. 0부터 주어진 숫자 N까지 SemiPrime인지 확인해서 배열로 저장한다.
- 초기값 0을 제외하고 1을 SemiPrime이 아닌 경우, 2를 SemiPrime인 경우로 설정한다.
- 0과 1의 경우는 SemiPrime이 아니니까 1로 초기화 시키고, 2부터 idx^2이 최대 정수 값인 주어진 정수 N 이하만큼 반복한다.
- 만일 해당 정수가 SemiPrime이 아닌 경우는 제외하고 계속 반복한다.
- 해당 정수와 제곱을 해당 값을 나눈 수가 SemiPrime이 아니라고 판단되지 않은 경우에 SemiPrime으로 설정하고, 그렇지 않은 경우 SemiPrime이 아닌 경우로 설정한다.
  * 제곱의 값을 나눈 특정 정수가 특정 배수인 경우는 특정 정수는 SemiPrime이 될 수 없다.
  * 위에서 SemiPrime이 되는 경우가 아닌 경우는 모두 SemiPrime이 아닌 정수이다.
- idx^2 값에 idx값을 더하여 N이하까지 반복하여 사전 합계를 계산하여 변수 preSum 배열로 저장한다.
  * idx 값을 더하면 idx 값의 배수로 계산이 반복 수행된다.
- 반복문을 통해 변수 preSum 배열을 활용하여 주어진 배열 P와 Q의 값 사이의 SemiPrime 갯수를 결과를 저장하는 result 배열로 저장한다.
- 반복이 끝나면 주어진 배열 P와 Q의 값 사이의 SemiPrime 갯수를 저장한 변수 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingKCBQY4-U9U/)

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/lesson11/CountSemiprimes.java)에서 확인 가능합니다.