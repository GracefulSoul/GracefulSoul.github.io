---
title: "Leetcode Java Largest Odd Number in String"
excerpt: "Leetcode Largest Odd Number in String Java"
last_modified_at: 2023-12-07T18:50:00
header:
  image: /assets/images/leetcode/largest-odd-number-in-string.png
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
[Link](https://leetcode.com/problems/largest-odd-number-in-string){:target="_blank"}

# 코드
```java
class Solution {

  public String largestOddNumber(String num) {
    int i = num.length();
    while (--i >= 0) {
      if (num.charAt(i) % 2 == 1) {
        return num.substring(0, i + 1);
      }
    }
    return "";
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-odd-number-in-string/submissions/1114259533/){:target="_blank"}

# 설명
1. num의 연속된 숫자들을 이용하여 가장 큰 홀수 숫자를 탐색하는 문제이다.

2. num의 역순부터 탐색하여 마지막 숫자가 홀수인 경우, num의 처음 위치부터 i번째 위치까지 주어진 문제의 결과로 반환한다.
- 재배열이 없이 num의 연속된 숫자가 가장 큰 홀수가 되는 경우는 마지막 위치가 홀수가 되는 위치라는 의미이다.

3. 반복이 완료되면 홀수가 존재하지 않으므로, ""을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestOddNumberInString.java){:target="_blank"}에서 확인 가능합니다.