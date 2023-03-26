---
title: "Leetcode Java Uncommon Words from Two Sentences"
excerpt: "Leetcode Uncommon Words from Two Sentences Java"
last_modified_at: 2023-03-26T12:50:00
header:
  image: /assets/images/leetcode/uncommon-words-from-two-sentences.png
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
[Link](https://leetcode.com/problems/uncommon-words-from-two-sentences){:target="_blank"}

# 코드
```java
class Solution {

  public String[] uncommonFromSentences(String s1, String s2) {
    Map<String, Integer> map = new HashMap<>();
    for (String word : s1.split(" ")) {
      map.put(word, map.getOrDefault(word, 0) + 1);
    }
    for (String word : s2.split(" ")) {
      map.put(word, map.getOrDefault(word, 0) + 1);
    }
    List<String> result = new ArrayList<>();
    for (String word : map.keySet()) {
      if (map.get(word) == 1) {
        result.add(word);
      }
    }
    return result.toArray(new String[result.size()]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/uncommon-words-from-two-sentences/submissions/922166294/){:target="_blank"}

# 설명
1. s1과 s2의 단어 중 중복되지 않은 단어를 찾는 문제이다.

2. map은 단어 별 반복 횟수를 저장할 변수로, s1과 s2를 공백(" ") 문자를 기준으로 분리하여 횟수를 계산한다.

3. result는 결과를 저장할 변수로, map을 반복하여 한 번만 사용된 문자를 넣어 배열로 전환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UncommonWordsFromTwoSentences.java){:target="_blank"}에서 확인 가능합니다.