---
title: "Leetcode Java Count Primes"
excerpt: "Leetcode Count Primes Java 풀이"
last_modified_at: 2021-10-08T12:00:00
header:
  image: /assets/images/leetcode/count-primes.png
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
[Link](https://leetcode.com/problems/count-primes/){:target="_blank"}

# 코드
```java
class Solution {

  public int countPrimes(int n) {
    if (n < 3) {
      return 0;
    }
    int result = n / 2;
    boolean[] notPrime = new boolean[n];
    for (int i = 3; i * i < n; i += 2) {
      if (notPrime[i]) {
        continue;
      }
      for (int j = i * i; j < n; j += 2 * i) {
        if (!notPrime[j]) {
          result--;
          notPrime[j] = true;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/567589481/){:target="_blank"}

# 설명
1. 주어진 정수 n 미만의 양의 정수 중 소수의 갯수를 구하는 문제이다.

2. 주어진 정수가 3 미만일 경우, 가장 작은 소수인 2를 포함하지 않으므로 0을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- result는 소수의 갯수를 저장하기 위한 변수로, $\frac{n}{2}$의 정수 값을 넣어준다.
  - 주어진 정수 n 미만의 소수의 갯수는 항상 $\frac{n}{2}$의 정수 값보다 같거나 작다.
  - 주어진 n이 5일 경우, 소수의 갯수는 2, 3로 2개이다.
  - 주어진 n이 10일 경우, 소수의 갯수는 2, 3, 5, 7로 4개이다.
  - 주어진 n이 20일 경우, 소수의 갯수는 2, 3, 5, 7, 11, 13, 17, 19로 8개 이다.
- notPrime은 소수가 아닌 값을 체크하기 위한 배열의 변수로, 주어진 정수 n의 사이즈로 초기화 한다.
  - boolean형의 초기 값은 false로, 모든 값이 소수가 아닌 것으로 체크를 한다.

4. 3 이상의 소수는 2 단위로 증가하기 때문에, 3부터 $i \times i$미만까지 2씩 증가시키며 반복을 수행한다.
- i가 소수인 경우, 반복을 계속 수행해준다.
- $i \times i$부터 n 전까지 $i \times 2$ 값들을 반복하며 아래를 수행한다.
  - 2의 배수인 값은 소수가 아니기 때문에, 소수의 갯수를 저장한 result의 값을 감소시킨다.
  - 위와 동일한 이유로 notPrime에 소수가 아닌 값(false)으로 저장한다.

5. 반복이 완료되면 주어진 정수 n 미만의 양의 정수 중 소수의 갯수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountPrimes.java){:target="_blank"}에서 확인 가능합니다.