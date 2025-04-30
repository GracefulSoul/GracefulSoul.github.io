---
title: "Leetcode Java Find Numbers with Even Number of Digits"
excerpt: "Leetcode - 'Find Numbers with Even Number of Digits' 문제 Java 풀이"
last_modified_at: 2025-04-30T08:50:00
header:
  image: /assets/images/leetcode/find-numbers-with-even-number-of-digits.png
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
[Link](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/){:target="_blank"}

# 코드
```java
class Solution {

  public int findNumbers(int[] nums) {
    int count = 0;
    for (int num : nums) {
      if ((9 < num && num < 100) || (999 < num && num < 10000) || num == 100000) {
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/submissions/1622352368/){:target="_blank"}

# 설명
1. nums 내 짝수 자리의 숫자 갯수를 계산하는 문제이다.

2. nums 내 아래 범위 내 짝수 자릿수인 숫자의 갯수를 계산하여 주어진 문제의 결과로 반환한다.
- [10, 99] 사이의 두 자리 숫자.
- [1000, 9999] 사이의 네 자리 숫자.
- 100000인 여섯 자리 숫자.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindNumbersWithEvenNumberOfDigits.java){:target="_blank"}에서 확인 가능합니다.