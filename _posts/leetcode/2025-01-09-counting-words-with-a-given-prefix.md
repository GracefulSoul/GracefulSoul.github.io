---
title: "Leetcode Java Counting Words With a Given Prefix"
excerpt: "Leetcode - 'Counting Words With a Given Prefix' 문제 Java 풀이"
last_modified_at: 2025-01-09T19:00:00
header:
  image: /assets/images/leetcode/counting-words-with-a-given-prefix.png
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
[Link](https://leetcode.com/problems/counting-words-with-a-given-prefix/){:target="_blank"}

# 코드
```java
class Solution {

  public int prefixCount(String[] words, String pref) {
    int result = 0;
    for (String word : words) {
      if (word.indexOf(pref) == 0) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/counting-words-with-a-given-prefix/submissions/1502797735/){:target="_blank"}

# 설명
1. words 중 pref로 시작하는 문자열의 갯수를 계산하는 문제이다.

2. result는 문자열의 갯수를 계산하기 위한 변수로, words의 각 문자열 중 pref가 시작 문자열 위치인 0을 만족하는 문자열의 갯수를 넣어준다.

3. 반복이 완료되면 조건을 만족하는 문자열의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountingWordsWithAGivenPrefix.java){:target="_blank"}에서 확인 가능합니다.