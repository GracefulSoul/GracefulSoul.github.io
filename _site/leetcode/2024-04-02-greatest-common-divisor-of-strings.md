---
title: "Leetcode Java Greatest Common Divisor of Strings"
excerpt: "Leetcode Greatest Common Divisor of Strings Java"
last_modified_at: 2024-04-02T18:05:00
header:
  image: /assets/images/leetcode/greatest-common-divisor-of-strings.png
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
[Link](https://leetcode.com/problems/greatest-common-divisor-of-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public String gcdOfStrings(String str1, String str2) {
    if (!(str1 + str2).equals(str2 + str1)) {
      return "";
    } else {
      return str2.substring(0, this.getGcd(str1.length(), str2.length()));
    }
  }

  private int getGcd(int a, int b) {
    return b == 0 ? a : this.getGcd(b, a % b);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/greatest-common-divisor-of-strings/submissions/1220962021/){:target="_blank"}

# 설명
1. 두 문자열 str1과 str2을 이용하여 str2 문자열로 str1 문자열을 나눌 때, 최대 길이의 문자열을 구하는 문제이다.
- 문자열 s는 "t"로 구성된 문자열 "ttt...tt" 문자열로, 해댕 문자열은 문자열 "t"로 문자열 s를 나눌 수 있다고 표현한다.

2. str1과 str2를 번갈아 앞뒤로 더한 문자열이 동일한지 여부에 따라 결과를 반환한다.
- 두 문자열이 동일하지 않으면 str2 문자열로 str1 문자열을 나눌 수 없으므로, 빈 문자열("")을 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니라면, str2의 처음부터 두 문자열의 길이의 최대 공약수 위치 이전까지 문자열을 잘라 주어진 문제의 결과로 반환한다.

# 해설
- 문자열을 나누는데 기준은 str1이 str2로 구성되어야 한다.
- 그렇기 때문에 두 문자열 str1과 str2을 앞뒤로 합친 결과가 동일해야 나눌 수 있다.
- 위의 경우가 아니라면, 두 문자열 str1과 str2의 길이에 대한 최대 공약수를 구하면 최소 중복을 제거한 최대 길이의 문자열을 구할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GreatestCommonDivisorOfStrings.java){:target="_blank"}에서 확인 가능합니다.