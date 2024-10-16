---
title: "Leetcode Java Longest String Chain"
excerpt: "Leetcode Longest String Chain Java"
last_modified_at: 2023-09-23T14:55:00
header:
  image: /assets/images/leetcode/longest-string-chain.png
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
[Link](https://leetcode.com/problems/longest-string-chain){:target="_blank"}

# 코드
```java
class Solution {

  public int longestStrChain(String[] words) {
    Map<String, Integer> map = new HashMap<>();
    Arrays.sort(words, (a, b) -> a.length() - b.length());
    int result = 0;
    for (String word : words) {
      int max = 0;
      for (int i = 0; i < word.length(); i++) {
        max = Math.max(max, map.getOrDefault(word.substring(0, i) + word.substring(i + 1), 0) + 1);
      }
      map.put(word, max);
      result = Math.max(result, max);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-string-chain/submissions/1056834832/){:target="_blank"}

# 설명
1. words 내 한 단어씩 붙여서 다음 단어를 만들 수 있는 문자열의 가장 많은 연결 문자열 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 문자열 별 연결 횟수를 저장하기 위한 변수로, HashMap으로 초기화한다.
- result는 가장 많은 연결 문자열의 갯수를 저장할 변수로, 0으로 초기화한다.

3. words를 짧은 문자열순으로 정렬한다.

4. words의 모든 문자열을 word에 넣고 아래를 반복한다.
- max는 word를 이용하여 가장 많은 연결 문자열의 갯수를 저장할 변수로, 0으로 초기화한다.
- 0부터 word의 길이 미만까지 i를 증가시키며 아래를 수행한다.
  - max에 max와 map에서 word의 처음부터 i번째 자리까지 문자열과 $i + 1$번째부터 끝까지 문자열을 이어준 key의 값을 꺼내 1을 더한 값 중 큰 값을 넣어준다.
- map에 word와 max를 넣어 word까지 최대 연결 횟수를 저장한다.
- result에 result와 max 중 가장 큰 값을 넣어준다.

5. 반복이 완료되면 가장 많은 연결 문자열의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestStringChain.java){:target="_blank"}에서 확인 가능합니다.