---
title: "Leetcode Java Longest Word in Dictionary through Deleting"
excerpt: "Leetcode Longest Word in Dictionary through Deleting Java"
last_modified_at: 2022-06-10T19:30:00
header:
  image: /assets/images/leetcode/longest-word-in-dictionary-through-deleting.png
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
[Link](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/){:target="_blank"}

# 코드
```java
class Solution {

  public String findLongestWord(String s, List<String> dictionary) {
    String result = "";
    for (String word : dictionary) {
      if ((word.length() > result.length() || (word.length() == result.length() && word.compareTo(result) < 0))
          && this.isSubsequence(word, s)) {
        result = word;
      }
    }
    return result;
  }

  private boolean isSubsequence(String str1, String str2) {
    int i = 0;
    int j = 0;
    while (i < str1.length() && j < str2.length()) {
      if (str1.charAt(i) == str2.charAt(j)) {
        i++;
      }
      j++;
    }
    return i == str1.length();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/718807766/){:target="_blank"}

# 설명
1. dictionary 중 s의 일부 문자를 제거하고 만들 수 있는 가장 긴 문자열을 찾는 문제이다.
- 동일한 길이의 문자열이 있는 경우, 사전 순서가 가장 작은(빠른) 순서의 단어를 반환한다.
- 만들 수 있는 문자열이 없는 경우, 빈 문자열("")을 반환한다.

2. 결과를 넣을 result를 빈 문자열("")로 초기화한다.

3. dictionary를 모두 순회하여 아래의 경우를 모두 만족하면, result에 word를 넣어준다.
- word의 길이가 result의 길이보다 길거나, word와 result의 길이가 같은 경우 word가 result보다 사전 순서가 빠른 경우 기본 조건을 만족한다.
- 4번에서 정의한 isSubsequence(String str1, String str2) 메서드를 만족한다.

4. s1이 s2의 부분 수열인지를 검증하기 위한 isSubsequence(String s1, String s2) 메서드를 정의한다.
- i는 s1의 위치 값을, j는 s2의 위치 값을 나타낼 변수로 0으로 초기화한다.
- i가 s1 길이 미만이고, j가 s2 길이 미만일 때 까지 아래를 반복한다.
  - s1의 i번째 문자가 s2의 j번째 문자와 동일한지 검증하면서 j를 증가시키고, 동일한 경우에만 i를 증가시킨다.
- 반복이 완료되면 i와 s1의 길이가 동일한지 검증하여, s1이 s2의 부분 수열에 속하는지 결과를 반환한다.

5. 반복이 완료되면 조건에 부합하는 단어를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestWordInDictionaryThroughDeleting.java){:target="_blank"}에서 확인 가능합니다.