---
title: "Leetcode Java Find the K-th Character in String Game I"
excerpt: "Leetcode - 'Find the K-th Character in String Game I' 문제 Java 풀이"
last_modified_at: 2025-07-03T18:55:00
header:
  image: /assets/images/leetcode/find-the-k-th-character-in-string-game-i.png
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
[Link](https://leetcode.com/problems/find-the-k-th-character-in-string-game-i/){:target="_blank"}

# 코드
```java
class Solution {

  public char kthCharacter(int k) {
    StringBuilder sb = new StringBuilder("a");
    while (sb.length() <= k) {
      int length = sb.length();
      for (int i = 0; i < length; i++) {
        sb.append((char) ('a' + ((sb.charAt(i) - 'a') + 1) % 26));
      }
    }
    return sb.charAt(k - 1);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-k-th-character-in-string-game-i/submissions/1684861326/){:target="_blank"}

# 설명
1. 아래 규칙대로 문자열을 만들 때, k번째 문자를 반환하는 문제이다.
- "a" 문자부터 시작해서 현재 문자열 내 모든 영문자들의 다음 순서의 영문자로 변환하여 이어주되, 'z' 문자의 다음 문자는 'a'로 순회한다.
- 예를 들어, "c"에서 연산을 수행하면 "cd"가 되고 "zb"에서 연산을 수행하면 "zbac"가 된다.

2. sb는 동적 문자열 생성을 위한 변수로, StringBuilder로 첫 값인 "a" 문자를 넣어 초기화한다.

3. sb의 길이가 k 이하일 때 까지 아래를 반복한다.
- length에 현재 sb의 길이를 넣어준다.
- 0부터 length 미만까지 i를 증가시키며, sb에 sb의 i번째 문자의 다음 영소문자를 이어준다.

4. 반복이 완료되면 sb 내 $k - 1$번째 값인 k번째 문자를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheKthCharacterInStringGameI.java){:target="_blank"}에서 확인 가능합니다.