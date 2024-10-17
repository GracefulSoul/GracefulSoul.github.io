---
title: "Leetcode Java Valid Anagram"
excerpt: "Leetcode - 'Valid Anagram' 문제 Java 풀이"
last_modified_at: 2021-11-18T20:00:00
header:
  image: /assets/images/leetcode/valid-anagram.png
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
[Link](https://leetcode.com/problems/valid-anagram/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isAnagram(String s, String t) {
    int[] alphabet = new int[26];
    for (char c : s.toCharArray()) {
      alphabet[c - 'a']++;
    }
    for (char c : t.toCharArray()) {
      alphabet[c - 'a']--;
    }
    for (int idx = 0; idx < alphabet.length; idx++) {
      if (alphabet[idx] != 0) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/589062480/){:target="_blank"}

# 설명
1. 주어진 문자열 s와 t를 이용하여 [아나그램(Anagram)](https://en.wikipedia.org/wiki/Anagram){:target="_blank"}인지 검증하는 문제이다.
- 아나그램(Anagram)이란 한 문자열을 재 배열하여 만드는 문자열이다.

2. 정수 배열인 alphabet을 영소문자의 개수인 26개 사이즈로 정의한다.

3. 주어진 문자열 s의 각 문자를 활용하여 alphabet 배열 내 각 위치의 값을 증가시킨다.
- s를 한 문자씩 떼어 'a'를 뺀 숫자는 a(0)~z(25)까지 존재하므로, 해당 위치의 값을 증가시켜 개수를 가산한다.

4. 주어진 문자열 t의 각 문자를 활용하여 alphabet 배열 내 각 위치의 값을 감소시킨다.
- s를 한 문자씩 떼어 'a'를 뺀 숫자는 a(0)~z(25)까지 존재하므로, 해당 위치의 값을 감소시켜 개수를 감산한다.

5. alphabet 배열을 처음부터 끝까지 확인하여 특정 위치의 값이 0이 아닌 경우 주어진 문자열 t는  s를 이용하여 아나그램으로 만들 수 없는 문자열이므로, 주어진 문제의 결과로 false를 반환한다.

6. 반복이 완료되면 주어진 문자열 t는  s를 이용하여 아나그램으로 만들 수 있는 문자열이므로, 주어진 문제의 결과로 true를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidAnagram.java){:target="_blank"}에서 확인 가능합니다.