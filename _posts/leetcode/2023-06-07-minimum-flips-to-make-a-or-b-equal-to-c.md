---
title: "Leetcode Java Minimum Flips to Make a OR b Equal to c"
excerpt: "Leetcode Minimum Flips to Make a OR b Equal to c Java"
last_modified_at: 2023-06-07T19:50:00
header:
  image: /assets/images/leetcode/minimum-flips-to-make-a-or-b-equal-to-c.png
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
[Link](https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c){:target="_blank"}

# 코드
```java
class Solution {

  public int minFlips(int a, int b, int c) {
    int result = 0;
    while (a > 0 || b > 0 || c > 0) {
      if ((c & 1) == 0) {
        result += (a & 1) + (b & 1);
      } else if ((a & 1) == 0 && (b & 1) == 0) {
        result++;
      }
      a >>= 1;
      b >>= 1;
      c >>= 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c/submissions/965838904/){:target="_blank"}

# 설명
1. a와 b의 OR 비트 연산의 결과가 c가 되기 위한 최소 플립 횟수를 구하는 문제이다.
- 플립은 비트가 0인 경우 1로, 1인 경우 0으로 바꾸는 행위이다.

2. result는 최소 플립 횟수를 저장할 변수로, 0으로 초기화 한다.

3. a와 b, c 하나라도 0 초과일 때 까지 아래를 반복한다.
- c와 1의 AND 비트 연산의 결과가 0인 경우, result에 a와 1의 AND 비트 연산 결과인 a를 플립하는 경우와 b와 1의 AND 비트 연산 결과인 b를 플립하는 경우의 합을 넣어준다.
- 위가 아니라 a와 1의 AND 비트 연산 결과가 0이고 b와 1의 AND 비트 연산 결과가 0인 경우, a와 b 둘 중 하나만 플립하면 되므로 result를 증가시켜준다.
- 현재 위치에서 플립 횟수를 계산했으므로 a와 b, c의 비트 값들을 우측으로 한 칸씩 이동시켜준다.

4. 반복이 완료되면 최소 플립 횟수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumFlipsToMakeAORBEqualToC.java){:target="_blank"}에서 확인 가능합니다.