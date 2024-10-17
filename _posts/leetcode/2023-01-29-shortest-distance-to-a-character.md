---
title: "Leetcode Java Shortest Distance to a Character"
excerpt: "Leetcode - 'Shortest Distance to a Character' 문제 Java 풀이"
last_modified_at: 2023-01-29T09:00:00
header:
  image: /assets/images/leetcode/shortest-distance-to-a-character.png
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
[Link](https://leetcode.com/problems/shortest-distance-to-a-character){:target="_blank"}

# 코드
```java
class Solution {

  public int[] shortestToChar(String s, char c) {
    int length = s.length();
    int[] result = new int[length];
    int prev = -length;
    for (int idx = 0; idx < length; idx++) {
      if (s.charAt(idx) == c) {
        prev = idx;
      }
      result[idx] = idx - prev;
    }
    for (int idx = prev - 1; idx >= 0; idx--) {
      if (s.charAt(idx) == c) {
        prev = idx;
      }
      result[idx] = Math.min(result[idx], prev - idx);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shortest-distance-to-a-character/submissions/887111161/){:target="_blank"}

# 설명
1. s의 각 문자에서 전후로 가장 가까운 c와의 거리를 모두 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 s의 길이를 저장한 변수이다.
- result는 각 문자 별 거리를 저장하기 위한 변수로, length 길이의 정수 배열로 초기화한다.
- prev는 이전 c가 발생한 위치를 저장할 변수로, 거리가 가장 긴 경우인 length를 음수로 전환하여 넣어준다.

3. s의 각 문자를 좌측에서 우측으로 탐색하며 거리를 측정한다.

4. s의 마지막 발생위치인 prev의 이전 위치부터 시작하여 우측에서 좌측으로 탐색하여 다시 거리를 확인한다.

5. 반복이 완료되면 각 문자 별 거리가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestDistanceToACharacter.java){:target="_blank"}에서 확인 가능합니다.