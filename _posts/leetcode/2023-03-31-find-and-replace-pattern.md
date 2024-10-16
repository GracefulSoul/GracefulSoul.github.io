---
title: "Leetcode Java Find and Replace Pattern"
excerpt: "Leetcode Find and Replace Pattern Java"
last_modified_at: 2023-03-31T19:40:00
header:
  image: /assets/images/leetcode/find-and-replace-pattern.png
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
[Link](https://leetcode.com/problems/find-and-replace-pattern){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> findAndReplacePattern(String[] words, String pattern) {
    List<String> result = new ArrayList<>();
    for (String word : words) {
      if (this.match(word, pattern)) {
        result.add(word);
      }
    }
    return result;
  }

  private boolean match(String word, String pattern) {
    for (int i = 0; i < word.length(); i++) {
      if (word.indexOf(word.charAt(i)) != pattern.indexOf(pattern.charAt(i))) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-and-replace-pattern/submissions/925311963/){:target="_blank"}

# 설명
1. words 내 단어들 중 pattern의 문자 패턴과 일치하는 문자를 찾는 문제이다.

2. result는 패턴과 일치하는 문자를 넣을 변수로, ArrayList로 초기화한다.

3. words를 반복하여 4번에서 정의한 match(String word, String pattern)를 만족하는지 검증하여 result에 넣어준다.

4. 문자열 검증을 위한 match(String word, String pattern) 메서드를 정의한다.
- 0부터 word의 길이 미만까지 i를 증가시키며 문자 별 위치가 동일한지 검증하여, 만족하지 않는 경우 false를 반환한다.
- 반복이 완료되어 패턴과 일치하면 true를 반환한다.

5. 반복이 완료되어 패턴과 일치하는 문자열만 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindAndReplacePattern.java){:target="_blank"}에서 확인 가능합니다.