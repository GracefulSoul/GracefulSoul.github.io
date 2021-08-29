---
title: "Leetcode Java Word Break II"
excerpt: "Leetcode Word Break II Java 풀이"
last_modified_at: 2021-08-29T14:00:00
header:
  image: /assets/images/leetcode/word-break-ii.png
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
[Link](https://leetcode.com/problems/word-break-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> wordBreak(String s, List<String> wordDict) {
    return this.recursive(s, wordDict, new HashMap<>());
  }

  private List<String> recursive(String s, List<String> wordDict, Map<String, List<String>> map) {
    if (map.containsKey(s)) {
      return map.get(s);
    } else {
      List<String> result = new ArrayList<>();
      for (String word : wordDict) {
        if (s.startsWith(word)) {
          String temp = s.substring(word.length());
          if (temp.length() == 0) {
            result.add(word);
          } else {
            for (String sub : this.recursive(temp, wordDict, map)) {
              result.add(String.join(" ", word, sub));
            }
          }
        }
      }
      map.put(s, result);
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/545907604/){:target="_blank"}

# 설명
1. 주어진 List wordDict를 이용하여 문자열 s를 만들 수 있는 모든 경우의 수를 찾는 문제이다.

2. 재귀 호출을 이용하여 map에 문자열을 저장하고, wordDict를 이용하여 문자열 s를 만들 수 있는 모든 경우의 수를 찾아 주어진 문제의 결과로 반환한다.
- 문제의 결과를 저장하기 위한 변수 result를 정의한다.
- map에 문자열 s가 존재하는 경우 저장한 문자열을 가져와 반환한다.
- map에 문자열 s가 존재하지 않는 경우 wordDict를 반복하여 아래의 문자열 검증을 수행한다.
  - 문자열 s가 word로 시작되는 경우, 해당 문자열을 잘라 temp를 정의한다.
  - temp의 길이가 0인 경우 result에 추가한다.
  - temp의 길이가 0이 아닌 경우, 재귀 호출을 이용하여 문자열을 조합하여 result에 추가한다.
- map에 결과를 저장하여 문자열을 임시 보관하고 결과를 저장한 result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WordBreakII.java){:target="_blank"}에서 확인 가능합니다.