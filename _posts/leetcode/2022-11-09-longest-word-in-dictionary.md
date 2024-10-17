---
title: "Leetcode Java Longest Word in Dictionary"
excerpt: "Leetcode - 'Longest Word in Dictionary' 문제 Java 풀이"
last_modified_at: 2022-11-09T19:30:00
header:
  image: /assets/images/leetcode/longest-word-in-dictionary.png
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
[Link](https://leetcode.com/problems/longest-word-in-dictionary){:target="_blank"}

# 코드
```java
class Solution {

  public String longestWord(String[] words) {
    String result = "";
    Set<String> set = new HashSet<>();
    for (String word : words) {
      set.add(word);
    }
    for (String word : words) {
      int wordLength = word.length();
      int longestLength = result.length();
      if (wordLength > longestLength || (wordLength == longestLength && word.compareTo(result) < 0)) {
        boolean isLongestWord = true;
        for (int idx = 1; idx < wordLength; idx++) {
          if (!set.contains(word.substring(0, idx))) {
            isLongestWord = false;
            break;
          }
        }
        if (isLongestWord) {
          result = word;
        }
      }
    }
    return result;
  }


}
```

# 결과
[Link](https://leetcode.com/submissions/detail/840021618/){:target="_blank"}

# 설명
1. words의 각 문자열들을 한 문자씩 사용하여 만들 수 있는 가장 긴 문자열의 길이인 문자열을 찾는 문제이다.
- 단어는 각 문자열의 한 문자씩 사용하여 왼쪽에서 오른쪽으로 이전까지 만들었던 문자열 끝에 앞의 문자를 붙이는 식으로 만들어야 한다.
- 둘 이상의 정답이 존재하는 경우, 사전순으로 긴 단어를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 가장 긴 문자열을 넣을 변수로, 빈 값으로 초기화한다.
- set은 words 내 문자열들을 중복 제거하여 저장할 변수로, HashSet으로 초기화하여 words의 모든 문자열을 넣어준다.

3. words의 모든 문자열을 word에 넣어 아래를 반복한다.
- wordLength에 word의 길이를, longestLength에 result의 길이를 넣어 초기화한다.
- wordLength가 longestLength보다 긴 경우이거나, 동일한 길이인 경우 word가 사전순 우선되는 단어인 경우 아래를 수행한다.
  - word의 처음부터 한 문자씩 붙인 부분 문자열이 words에 포함되지 않는 경우, 조건에 해당하지 않으므로 isLongestWord를 false로 바꾸고 반복을 중지한다.
- isLongestWord가 true인 경우만 result에 word를 넣어준다.

4. 반복이 완료되면 조건을 만족하는 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestWordInDictionary.java){:target="_blank"}에서 확인 가능합니다.