---
title: "Leetcode Java Largest Palindrome Product"
excerpt: "Leetcode Largest Palindrome Product Java 풀이"
last_modified_at: 2022-05-06T12:00:00
header:
  image: /assets/images/leetcode/largest-palindrome-product.png
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
[Link](https://leetcode.com/problems/largest-palindrome-product/){:target="_blank"}

# 코드
```java
class Solution {

  public int largestPalindrome(int n) {
    if (n > 1) {
      int num = (int) Math.pow(10, n);
      for (long idx = 2; idx < num; idx += 2) {
        long high = num - idx;
        long low = Long.parseLong(new StringBuilder(Long.toString(high)).reverse().toString());
        long temp = (idx * idx) - (4 * low);
        if (temp < 0) {
          continue;
        }
        long sqrt = (long) Math.sqrt(temp);
        if (sqrt * sqrt == temp) {
          return (int) (((high * num) + low) % 1337);
        }
      }
    }
    return 9;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/694013045/){:target="_blank"}

# 설명
1. n자리의 두 숫자의 곱이 회문이 되는 가장 큰 값을 찾아 1337을 나눈 나머지를 반환하는 문제이다.

2. n이 1인 경우, 한 자리의 숫자 중 가장 큰 숫자인 9를 주어진 문제의 결과로 반환한다.

3. num에 10의 n승한 결과를 넣고, 2부터 num 미만까지 idx를 2씩 증가시키며 반복을 수행한다.
- high에 $num - idx$를, low에는 high를 거꾸로 뒤집어 넣어준다.
  - 회문이 되는 결과를 절반으로 나누면 첫 번째 값의 거꾸로 된 값이 두 번째 값이 되므로, 이 값을 만들어 검증을 수행하는 것이다.
- temp에 idx의 제곱에 $4 \times low$를 뺀 값을 넣고, temp가 0 미만인 경우 검증을 수행 할 수 없으므로 다음 반복을 수행한다.
- temp가 정상적인 제곱수인 경우, $(high \times num) + low$ 값이 두 값의 곱으로 완성 가능한 수이므로 1337을 나눈 나머지 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestPalindromeProduct.java){:target="_blank"}에서 확인 가능합니다.