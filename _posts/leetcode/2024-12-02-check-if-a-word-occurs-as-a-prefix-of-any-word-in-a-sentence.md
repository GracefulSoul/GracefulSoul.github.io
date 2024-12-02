---
title: "Leetcode Java Check If a Word Occurs As a Prefix of Any Word in a Sentence"
excerpt: "Leetcode - 'Check If a Word Occurs As a Prefix of Any Word in a Sentence' 문제 Java 풀이"
last_modified_at: 2024-12-02T18:30:00
header:
  image: /assets/images/leetcode/check-if-a-word-occurs-as-a-prefix-of-any-word-in-a-sentence.png
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
[Link](https://leetcode.com/problems/check-if-a-word-occurs-as-a-prefix-of-any-word-in-a-sentence/){:target="_blank"}

# 코드
```java
class Solution {

  public int isPrefixOfWord(String sentence, String searchWord) {
    String[] words = sentence.split(" ");
    for (int i = 0; i < words.length; i++) {
      if (words[i].startsWith(searchWord)) {
        return i + 1;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-a-word-occurs-as-a-prefix-of-any-word-in-a-sentence/submissions/1468170667/){:target="_blank"}

# 설명
1. sentence의 단어들 중 searchWord로 시작하는 단어의 위치를 1-index로 반환하는 문제이다.
- 단, searchWrod로 시작하는 단어가 존재하지 않으면 -1을 주어진 문제의 결과로 반환한다.

2. words는 sentence를 띄어쓰기(" ") 단위로 분리하여 저장한 문자열 배열이다.

3. 0부터 words 길이 미만까지 i를 증가시키며 아래를 반복한다.
- words[i]가 searchWrod로 시작하는 경우, $i + 1$을 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 searchWrod로 시작하는 단어가 존재하지 않으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfAWordOccursAsAPrefixOfAnyWordInASentence.java){:target="_blank"}에서 확인 가능합니다.