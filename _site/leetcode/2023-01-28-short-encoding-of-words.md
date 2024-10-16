---
title: "Leetcode Java Short Encoding of Words"
excerpt: "Leetcode Short Encoding of Words Java"
last_modified_at: 2023-01-28T09:30:00
header:
  image: /assets/images/leetcode/short-encoding-of-words.png
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
[Link](https://leetcode.com/problems/short-encoding-of-words){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumLengthEncoding(String[] words) {
    Set<String> set = new HashSet<>(Arrays.asList(words));
    for (String word : words) {
      for (int idx = 1; idx < word.length(); idx++) {
        set.remove(word.substring(idx));
      }
    }
    int result = 0;
    for (String word : set) {
      result += word.length() + 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/short-encoding-of-words/submissions/886557992/){:target="_blank"}

# 설명
1. words 내 문자열들로 아래의 규칙을 만족하는 인코딩의 최소 길이를 구하는 문제이다.
- 인코딩은 참조 문자열을 이용하여 각 문자열 뒤에 '#' 문자열을 붙여 만드는 문자열 형식이다.
- 참조 문자열이란 words 내 특정 단어가 해당 문자열을 제외한 다른 문자열에 포함되지 않는 문자열이다.

2. set에 words의 중복된 단어를 제거하기 위해 HashSet으로 words의 문자열을 넣어준다.

3. words를 반복하여 각 문자열이 words 내 문자열들 중 하나라도 포함되는지 검증하여 set에서 제거해준다.

4. result에 set 내 각 문자열의 길이와 '#' 문자열의 길이인 1을 더한 값을 누계하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortEncodingOfWords.java){:target="_blank"}에서 확인 가능합니다.