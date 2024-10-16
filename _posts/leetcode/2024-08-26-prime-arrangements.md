---
title: "Leetcode Java Prime Arrangements"
excerpt: "Leetcode Prime Arrangements Java"
last_modified_at: 2024-08-26T18:50:00
header:
  image: /assets/images/leetcode/prime-arrangements.png
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
[Link](https://leetcode.com/problems/prime-arrangements/){:target="_blank"}

# 코드
```java
class Solution {

  public int numPrimeArrangements(int n) {
    boolean[] primes = new boolean[n + 1];
    Arrays.fill(primes, 2, n + 1, true);
    for (int i = 2; i * i <= n; i++) {
      if (primes[i]) {
        for (int j = i * i; j <= n; j += i) {
          primes[j] = false;
        }
      }
    }
    int count = 0;
    for (boolean prime : primes) {
      if (prime) {
        count++;
      }
    }
    long result = 1;
    for (int i = 2; i <= count; i++) {
      result = (result * i) % 1000000007;
    }
    for (int i = 2; i <= n - count; i++) {
      result = (result * i) % 1000000007;
    }
    return (int) result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/prime-arrangements/submissions/1368795070/){:target="_blank"}

# 설명
1. 소수가 소수 지수가 되도록 1부터 n까지 순열의 수를 반환하는 문제이다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- primes는 각 위치가 소수인지 저장할 변수로, $n + 1$ 크기의 부울 변수로 초기화하여 소수가 아닌 위치에 false를 넣어준다.
- count는 소수의 갯수를 저장할 변수로, primes를 반복하여 소수의 갯수를 저장해준다.
- result는 결과 값을 저장할 변수로, long형의 1로 초기화한다.

3. 아래의 각 경우를 이용하여 순열의 수를 계산 후 result를 int형으로 변경하여 주어진 문제의 결과로 반환한다.
- 소수인 값들을 연속으로 나열하는 경우인 2부터 count 이하까지 i를 증가시키며, result에 $result \times i$에 모듈러 $10^9 + 7$를 적용한 결과를 넣어준다.
- 수사가 아닌 값들을 연속으로 나열하는 경우인 2부터 $n - count$ 이하까지 i를 증가시키며, result에 $result \times i$에 모듈러 $10^9 + 7$를 적용한 결과를 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PrimeArrangements.java){:target="_blank"}에서 확인 가능합니다.