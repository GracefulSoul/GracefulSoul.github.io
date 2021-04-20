---
title: "Codility Java CountNonDivisible"
excerpt: "Lesson11. Sieve Of Eratosthenes"
last_modified_at: 2021-03-06T20:22:00
header:
  image: /assets/images/codility/lesson11/CountNonDivisible.png
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
[Link](https://app.codility.com/programmers/lessons/11-sieve_of_eratosthenes/count_non_divisible/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int[] solution(int[] A) {
    int[] result = new int[A.length];
    // Initializing array, element's range is [1, 2 * N]
    int[] divisors = new int[(A.length * 2) + 1];
    for (int idx = 0; idx < A.length; idx++) {
      divisors[A[idx]]++;
    }
    for (int idx1 = 0; idx1 < A.length; idx1++) {
      int count = 0;
      for (int idx2 = 1; idx2 * idx2 <= A[idx1]; idx2++) {
        // Common factor
        if (A[idx1] % idx2 == 0) {
          count += divisors[idx2];
          // Not square root
          if (A[idx1] / idx2 != idx2) {
            count += divisors[A[idx1] / idx2];
          }
        }
      }
      result[idx1] = A.length - count;
    }
    return result;
  }
}
```

# 설명
1. 주어진 배열 A에 존재하는 정수의 숫자 별 갯수를 변수 divisors 배열에 저장한다.
- 숫자는 1부터 2 * N까지 주어지므로, 0을 제외하면 배열의 크기는 (2 * N) + 1이어야 한다.
2. 주어진 배열 A를 변수 divisors를 이용하여 인수가 아닌 숫자의 수를 구한다.
- divisors 배열은 숫자 기준으로 저장되었으므로 0번째 인덱스는 무시한다.
- 최대 반복은 제곱근이 될 수 있는 idx2^2가 A[idx1] 이하가 될 때까지 한다.
- 반복 중 나머지가 0이 되면 인수가 되는 숫자이다.
- 만일 A[idx1] / idx2가 idx2가 되는 경우는 제곱근이 되는 경우이므로, 한 번을 더 더해준다.
- 마지막으로 A의 크기에서 인수가 되는 숫자의 갯수를 빼면, 인수가 아닌 숫자의 갯수가 나오므로 해당 결과를 변수 result에 저장한다.
3. 반복이 끝나면 주어진 배열 A의 각 숫자의 인수가 아닌 숫자의 갯수를 저장한 변수 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingVZ25BY-FPX/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson11/CountNonDivisible.java){:target="_blank"}에서 확인 가능합니다.