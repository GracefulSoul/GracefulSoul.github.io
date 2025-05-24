---
title: "Leetcode Java Find Words Containing Character"
excerpt: "Leetcode - 'Find Words Containing Character' 문제 Java 풀이"
last_modified_at: 2025-05-24T22:55:00
header:
  image: /assets/images/leetcode/find-words-containing-character.png
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
[Link](https://leetcode.com/problems/find-words-containing-character/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> findWordsContaining(String[] words, char x) {
    List<Integer> result = new ArrayList<>();
    for (int i = 0; i < words.length; i++) {
      if (words[i].indexOf(x) != -1) {
        result.add(i);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-words-containing-character/submissions/1643050056/){:target="_blank"}

# 설명
1. words 내 x 문자가 포함된 문자의 위치를 모두 반환하는 문제이다.

2. result는 결과를 저장할 변수로, ArrayList로 초기화한다.

3. 0부터 words의 길이 미만까지 i를 증가시키며, words[i]의 문자열에 x 문자가 -1이 아닌 포함되면 result에 위치 값인 i를 넣어준다.

4. 반복이 완료되면 위치 값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindWordsContainingCharacter.java){:target="_blank"}에서 확인 가능합니다.