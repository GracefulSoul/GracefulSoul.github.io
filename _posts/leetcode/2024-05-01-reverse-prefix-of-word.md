---
title: "Leetcode Java Reverse Prefix of Word"
excerpt: "Leetcode Easy - 'Reverse Prefix of Word' 문제 Java 풀이"
last_modified_at: 2024-05-01T10:20:00
header:
  image: /assets/images/leetcode/reverse-prefix-of-word.png
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
[Link](https://leetcode.com/problems/reverse-prefix-of-word/){:target="_blank"}

# 코드
```java
class Solution {

  public String reversePrefix(String word, char ch) {
    int index = word.indexOf(ch);
    if (index == -1) {
      return word;
    } else {
      return new StringBuilder(word.substring(0, index + 1)).reverse().toString() + word.substring(index + 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reverse-prefix-of-word/submissions/1246117721/){:target="_blank"}

# 설명
1. word 내 첫 ch 문자 위치까지의 문자열을 거꾸로 뒤집는 문제이다.

2. index는 word의 ch 위치를 저장할 변수로, -1인 경우 word를 그대로 주어진 문제의 결과로 반환한다.

3. 위의 경우가 아니라면 word의 처음부터 index까지의 문자열을 거꾸로 뒤집고 나머지 문자열을 이어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReversePrefixOfWord.java){:target="_blank"}에서 확인 가능합니다.