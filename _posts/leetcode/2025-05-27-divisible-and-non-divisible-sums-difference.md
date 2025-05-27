---
title: "Leetcode Java Divisible and Non-divisible Sums Difference"
excerpt: "Leetcode - 'Divisible and Non-divisible Sums Difference' 문제 Java 풀이"
last_modified_at: 2025-05-27T19:05:00
header:
  image: /assets/images/leetcode/divisible-and-non-divisible-sums-difference.png
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
[Link](https://leetcode.com/problems/divisible-and-non-divisible-sums-difference/){:target="_blank"}

# 코드
```java
class Solution {

  public int differenceOfSums(int n, int m) {
    int result = 0;
    for (int i = 1; i <= n; i++) {
      if (i % m == 0) {
        result -= i;
      } else {
        result += i;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/divisible-and-non-divisible-sums-difference/submissions/1645883840/){:target="_blank"}

# 설명
1. [1, n] 범위의 숫자들 중 m로 나눈 나머지가 0이 아닌 값의 합에 0인 값의 합을 뺀 결과를 구하는 문제이다.

2. result는 결과를 저장할 변수로, 0으로 초기화한다.

3. 1부터 n 이하까지 i를 증가시키며 아래를 반복한다.
- i를 m으로 나눈 나머지가 0인 m의 배수인 경우, result에 i를 빼준다.
- i를 m으로 나눈 나머지가 0이 아닌 경우, result에 i를 더해준다.

4. 반복이 완료되면 합계가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DivisibleAndNonDivisibleSumsDifference.java){:target="_blank"}에서 확인 가능합니다.