---
title: "Leetcode Java Subtract the Product and Sum of Digits of an Integer"
excerpt: "Leetcode - 'Subtract the Product and Sum of Digits of an Integer' 문제 Java 풀이"
last_modified_at: 2025-08-04T18:40:00
header:
  image: /assets/images/leetcode/subtract-the-product-and-sum-of-digits-of-an-integer.png
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
[Link](https://leetcode.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/){:target="_blank"}

# 코드
```java
class Solution {

  public int subtractProductAndSum(int n) {
    int substract = 1;
    int sum = 0;
    while (n > 0) {
      int remainder = n % 10;
      n /= 10;
      substract *= remainder;
      sum += remainder;
    }
    return substract - sum;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/submissions/1722878217/){:target="_blank"}

# 설명
1. n의 각 자리의 숫자들을 곱한 값에 합한 값을 뺀 값을 반환하는 문제이다.

2. substract는 곱한 값을 sum은 더한 값을 저장할 변수로, 1과 0으로 초기화한다.

3. n이 0 초과일 때까지 아래를 반복한다.
- remainder에 n을 10으로 나눈 나머지 값을 저장한다.
- n을 10으로 나눈 몫을 넣어준다.
- substract에 방금 자릿수인 remainder 값을 자기 자신과 곱한 값을 넣어준다.
- sum에 동일하게 방금 자릿수인 remainder 값을 더해준다.

4. 반복이 완료되면 $substract - sum$의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SubtractTheProductAndSumOfDigitsOfAnInteger.java){:target="_blank"}에서 확인 가능합니다.