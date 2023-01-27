---
title: "Leetcode Java Most Common Word"
excerpt: "Leetcode Most Common Word Java"
last_modified_at: 2023-01-27T20:20:00
header:
  image: /assets/images/leetcode/most-common-word.png
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
[Link](https://leetcode.com/problems/most-common-word){:target="_blank"}

# 코드
```java
class Solution {

  public String mostCommonWord(String paragraph, String[] banned) {
    Set<String> banList = new HashSet<>(Arrays.asList(banned));
    String[] words = paragraph.replaceAll("\\W+", " ").toLowerCase().split("\\s+");
    Map<String, Integer> map = new HashMap<>();
    for (String word : words) {
      if (!banList.contains(word)) {
        map.put(word, map.getOrDefault(word, 0) + 1);
      }
    }
    return Collections.max(map.entrySet(), Map.Entry.comparingByValue()).getKey();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/most-common-word/submissions/886229905/){:target="_blank"}

# 설명
1. paragraph에서 banned에 존재하는 문자열을 제외하고 가장 많이 발생한 문자열을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- banList는 banned를 중복을 제거하여 저장한 변수이다.
- words는 paragraph를 특수 문자들을 제거한 문자 배열로 저장한 변수이다.
- map은 words 내 문자열 갯수를 세기 위한 변수로, HashMap으로 초기화하여 words를 반복하여 banList에 없는 word를 키 발생 횟수를 값으로 계산하여 넣어준다.

3. map에서 가장 많이 발생한 변수의 키를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MostCommonWord.java){:target="_blank"}에서 확인 가능합니다.