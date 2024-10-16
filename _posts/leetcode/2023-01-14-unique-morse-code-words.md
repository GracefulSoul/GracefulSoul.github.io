---
title: "Leetcode Java Unique Morse Code Words"
excerpt: "Leetcode Unique Morse Code Words Java"
last_modified_at: 2023-01-14T08:30:00
header:
  image: /assets/images/leetcode/unique-morse-code-words.png
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
[Link](https://leetcode.com/problems/unique-morse-code-words){:target="_blank"}

# 코드
```java
class Solution {

  private static String[] LETTERS = new String[] {
    ".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..", ".---", "-.-", ".-..", "--", "-.", "---",
    ".--.", "--.-", ".-.", "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--.."
  };
  
  public int uniqueMorseRepresentations(String[] words) {
    Set<String> set = new HashSet<>();
    for (String word : words) {
      StringBuilder sb = new StringBuilder();
      for (char c : word.toCharArray()) {
        sb.append(LETTERS[c - 'a']);
      }
      set.add(sb.toString());
    }
    return set.size();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/unique-morse-code-words/submissions/877714815/){:target="_blank"}

# 설명
1. words의 문자열들의 각 문자들을 정의된 문장으로 모두 변경하였을 경우, 고유 문자열의 개수를 구하는 문제이다.

2. set은 고유 문자열의 개수를 저장할 변수로, HashSet으로 초기화한다.

3. words의 모든 단어를 word에 순차적으로 넣어 아래를 반복한다.
- sb는 word의 각 문자들을 주어진 문자열로 변환하여 저장할 변수로, 동적인 문자열 생성을 위해 StringBuilder로 정의한다.
- word의 각 문자들을 순차적으로, sb에 LETTERS의 해당 알파벳 순서에 해당하는 문자열로 이어준다.
- set에 sb를 문자열로 변환하여 추가해준다.

4. 변환된 고유 문자열이 저장된 set의 크기를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniqueMorseCodeWords.java){:target="_blank"}에서 확인 가능합니다.