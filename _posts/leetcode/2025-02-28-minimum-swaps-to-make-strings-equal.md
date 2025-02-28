---
title: "Leetcode Java Minimum Swaps to Make Strings Equal"
excerpt: "Leetcode - 'Minimum Swaps to Make Strings Equal' 문제 Java 풀이"
last_modified_at: 2025-02-28T11:00:00
header:
  image: /assets/images/leetcode/minimum-swaps-to-make-strings-equal.png
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
[Link](https://leetcode.com/problems/minimum-swaps-to-make-strings-equal/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumSwap(String s1, String s2) {
    char[] s1CharArray = s1.toCharArray();
    char[] s2CharArray = s2.toCharArray();
    int x = 0;
    int y = 0;
    for (int i = s1.length() - 1; i >= 0; i--) {
      if (s1CharArray[i] == 'x' && s2CharArray[i] == 'y') {
        x++;
      } else if (s1CharArray[i] == 'y' && s2CharArray[i] == 'x') {
        y++;
      }
    }
    if (x % 2 != y % 2) {
      return -1;
    } else {
      int result = (x / 2) + (y / 2);
      if (x % 2 == 1) {
        result += 2;
      }
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-swaps-to-make-strings-equal/submissions/1557718843/){:target="_blank"}

# 설명
1. s1과 s2 문자열의 문자를 스왑하여 동일한 문자열로 변환하기 위한 최소 횟수를 구하는 문제이다.
- 단, 변환이 불가능하면 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- s1CharArray와 s2CharArray는 s1과 s2를 문자 배열로 변환한 변수이다.
- x와 y는 s1에서 s2의 동일한 위치의 문자 중 x와 y가 다른 갯수를 저장할 변수로, 0으로 초기화하고 s1과 s2의 동일 자리의 문자가 다른 갯수를 계산해 넣어준다.

3. x와 y의 짝수 혹은 홀수로 동일하지 않은 동일한 문자열로 변환이 불가능한 경우, -1을 주어진 문제의 결과로 반환한다.

4. result에 $\frac{x}{2} + \frac{y}{2}$의 값을 넣어주고, x가 홀수인 문자 스왑을 추가해야 하는 경우에는 result에 2를 더 증가시킨 후 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumSwapsToMakeStringsEqual.java){:target="_blank"}에서 확인 가능합니다.