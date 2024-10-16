---
title: "Leetcode Java Longest Happy String"
excerpt: "Leetcode Longest Happy String Java"
last_modified_at: 2024-10-16T18:50:00
header:
  image: /assets/images/leetcode/longest-happy-string.png
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
[Link](https://leetcode.com/problems/longest-happy-string/){:target="_blank"}

# 코드
```java
class Solution {

  public String longestDiverseString(int a, int b, int c) {
    StringBuilder sb = new StringBuilder();
    int length = a + b + c;
    int countA = 0;
    int countB = 0;
    int countC = 0;
    for (int i = 0; i < length; i++) {
      if ((a >= b && a >= c && countA != 2) || (countB == 2 && a > 0) || (countC == 2 && a > 0)) {
        sb.append("a");
        a--;
        countA++;
        countB = countC = 0;
      } else if ((b >= a && b >= c && countB != 2) || (countA == 2 && b > 0) || (countC == 2 && b > 0)) {
        sb.append("b");
        b--;
        countB++;
        countA = countC = 0;
      } else if ((c >= a && c >= b && countC != 2) || (countA == 2 && c > 0) || (countB == 2 && c > 0)) {
        sb.append("c");
        c--;
        countC++;
        countA = countB = 0;
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-happy-string/submissions/1424126413/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 문자열을 만드는 문제이다.
- 'a', 'b', 'c'는 각자 세 번 이상 반복될 수 없다.
- s에는 'a', 'b', 'c'가 최대 a, b, c번 사용된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 동적으로 문자열을 구성하기 위한 변수로, StringBuilder로 초기화한다.
- length는 문자열의 최대 길이인 $a + b + c$를 저장한 변수이다.
- countA, countB, countC는 'a', 'b', 'c'의 연속된 갯수를 저장한 변수로, 모두 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- 아래 중 하나라도 만족하는 경우, sb에 "a"를 이어준 후 a를 감소시키고, countA를 증가, countB와 countC를 0으로 초기화한다.
  - a가 b와 c보다 크거나 같으면서 countA가 2가 아닌 "a"를 더 이어줄 수 있는 경우.
  - countB가 2이면서 a가 0보다 커서 "a"로 "b"의 연속을 끊어야하는 경우.
  - countC가 2이면서 a가 0보다 커서 "a"로 "c"의 연속을 끊어야하는 경우.
- 위의 경우가 아니면서 아래 중 하나라도 만족하는 경우, sb에 "b"를 이어준 후 b를 감소시키고, countB를 증가, countA와 countC를 0으로 초기화한다.
  - b가 a와 c보다 크거나 같으면서 countB가 2가 아닌 "b"를 더 이어줄 수 있는 경우.
  - countA가 2이면서 b가 0보다 커서 "b"로 "a"의 연속을 끊어야하는 경우.
  - countC가 2이면서 b가 0보다 커서 "b"로 "c"의 연속을 끊어야하는 경우.
- 위의 경우가 아니면서 아래 중 하나라도 만족하는 경우, sb에 "c"를 이어준 후 c를 감소시키고, countC를 증가, countA와 countB를 0으로 초기화한다.
  - c가 a와 c보다 크거나 같으면서 countC가 2가 아닌 "c"를 더 이어줄 수 있는 경우.
  - countA가 2이면서 c가 0보다 커서 "c"로 "a"의 연속을 끊어야하는 경우.
  - countB가 2이면서 c가 0보다 커서 "c"로 "b"의 연속을 끊어야하는 경우.  

4. 위의 반복이 완료되어 완성된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestHappyString.java){:target="_blank"}에서 확인 가능합니다.