---
title: "Leetcode Java Sum of Digits of String After Convert"
excerpt: "Leetcode Easy - 'Sum of Digits of String After Convert' 문제 Java 풀이"
last_modified_at: 2024-09-03T18:00:00
header:
  image: /assets/images/leetcode/sum-of-digits-of-string-after-convert.png
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
[Link](https://leetcode.com/problems/sum-of-digits-of-string-after-convert/){:target="_blank"}

# 코드
```java
class Solution {

  public int getLucky(String s, int k) {
    int result = 0;
    for (char c : s.toCharArray()) {
      int num = c - 96;
      if (num > 9) {
        result += (num / 10) + (num % 10);
      } else {
        result += num;
      }
    }
    while (--k > 0 && result > 9) {
      int sum = 0;
      while (result > 0) {
        sum += result % 10;
        result /= 10;
      }
      result = sum;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sum-of-digits-of-string-after-convert/submissions/1377488412/){:target="_blank"}

# 설명
1. 주어진 문자열 s의 영문자 순서(1부터 시작)를 순서대로 이어준 후, k번 각 자리 숫자를 더해준 결과를 반환하는 문제이다.

2. result는 결과를 저장할 변수로, 0으로 초기화 후 아래를 수행한다.
- s의 각 문자를 순서대로 c에 넣어 96을 뺀 1부터 시작하는 영문자 순서를 이용하여 result에 각 자리 숫자를 더해준다.

3. k를 감춘 값이 0보다 크거나 result가 9 초과인 2자리 수일 때 까지 아래를 반복한다.
- sum은 result의 각 자리 숫자를 더해줄 변수로, result가 0 초과일 때 까지 sum에 result를 10을 나눈 나머지 값을 더해준 후 result에 10을 나눈 몫을 넣어준다.
- result에 각 자리수를 더한 sum을 넣어준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfDigitsOfStringAfterConvert.java){:target="_blank"}에서 확인 가능합니다.