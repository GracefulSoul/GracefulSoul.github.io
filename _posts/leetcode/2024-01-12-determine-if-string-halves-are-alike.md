---
title: "Leetcode Java Determine if String Halves Are Alike"
excerpt: "Leetcode Easy - 'Determine if String Halves Are Alike' 문제 Java 풀이"
last_modified_at: 2024-01-12T10:10:00
header:
  image: /assets/images/leetcode/determine-if-string-halves-are-alike.png
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
[Link](https://leetcode.com/problems/determine-if-string-halves-are-alike){:target="_blank"}

# 코드
```java
class Solution {

  public boolean halvesAreAlike(String s) {
    String vowels = "aeiouAEIOU";
    int a = 0;
    int b = 0;
    for (int i = 0, j = s.length() - 1; i < j; i++, j--) {
      a += vowels.indexOf(s.charAt(i)) > -1 ? 1 : 0;
      b += vowels.indexOf(s.charAt(j)) > -1 ? 1 : 0;
    }
    return a == b;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/determine-if-string-halves-are-alike/submissions/1143780226/){:target="_blank"}

# 설명
1. 문자열 s를 절반으로 나누었을 때, 전반부와 후반부 내 모음의 갯수가 동일한지 검증하는 문제이다.
- 모음은 'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'로 구성된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- vowels는 모음을 저장한 변수로, 모음을 모두 모아 'aeiouAEIOU'로 초기화한다.
- a와 b는 전반부와 후반부의 모음 갯수로, 둘 다 0으로 초기화한다.

3. i가 0, j가 s의 길이보다 1 작은 값부터 i가 j보다 작을 때 까지 i를 증가, j를 감소시키며 s의 전반부와 후반부 문자의 갯수를 계산하여 a와 b에 넣어준다.

4. a와 b가 동일한지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DetermineIfStringHalvesAreAlike.java){:target="_blank"}에서 확인 가능합니다.