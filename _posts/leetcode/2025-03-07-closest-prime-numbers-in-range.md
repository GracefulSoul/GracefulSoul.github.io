---
title: "Leetcode Java Closest Prime Numbers in Range"
excerpt: "Leetcode - 'Closest Prime Numbers in Range' 문제 Java 풀이"
last_modified_at: 2025-03-07T19:10:00
header:
  image: /assets/images/leetcode/closest-prime-numbers-in-range.png
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
[Link](https://leetcode.com/problems/closest-prime-numbers-in-range/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] closestPrimes(int left, int right) {
    List<Integer> primes = new ArrayList<>();
    for (int i = left; i <= right; i++) {
      if (2 < i && i % 2 == 0) {
        continue;
      }
      if (this.isPrime(i)) {
        if (!primes.isEmpty() && i <= primes.get(primes.size() - 1) + 2) {
          return new int[] { primes.get(primes.size() - 1), i };
        }
        primes.add(i);
      }
    }
    if (primes.size() < 2) {
      return new int[] { -1, -1 };
    }
    int[] result = new int[2];
    int min = Integer.MAX_VALUE;
    for (int i = 1; i < primes.size(); i++) {
      int diff = primes.get(i) - primes.get(i - 1);
      if (diff < min) {
        min = diff;
        result[0] = primes.get(i - 1);
        result[1] = primes.get(i);
      }
    }
    return result;
  }

  private boolean isPrime(int number) {
    if (number == 1) {
      return false;
    } else {
      for (int i = 2; i <= (int) Math.sqrt(number); i++) {
        if (number % i == 0) {
          return false;
        }
      }
      return true;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/closest-prime-numbers-in-range/submissions/1565858608/){:target="_blank"}

# 설명
1. [left, right] 범위 내 값들 중 가장 인접한 두 소수값을 배열로 반환하는 문제이다.
- 단, 소수가 2개 미만이면 -1을 배열 값에 모두 넣어 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- primes는 소수값을 넣을 변수로, ArrayList로 초기화하여 left부터 right까지 범위 내 소수값들을 전부 넣어준다.
  - 단, primes의 크기가 2 미만으로 결과가 존재하지 않으면 -1로 채운 2 크기의 정수 배열을 주어진 문제의 결과로 반환한다.
- result는 결과를 저장할 변수로, 2 크기의 정수 배열로 초기화한다.
- min은 인접한 소수값의 차이가 최소인 값을 저장할 변수로, 정수의 가장 큰 값으로 초기화한다.

3. 1부터 primes의 크기 미만까지 i를 증가시키며 아래를 반복한다.
- diff에 primes의 i번째 값과 $i - 1$번째 값의 차잇값을 저장한다.
- diff가 min 미만인 최솟값인 경우, min에 diff, result에 위 두 값을 작은 순서대로 넣어준다.

4. 반복이 완료되어 가장 인접한 두 소수값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ClosestPrimeNumbersInRange.java){:target="_blank"}에서 확인 가능합니다.