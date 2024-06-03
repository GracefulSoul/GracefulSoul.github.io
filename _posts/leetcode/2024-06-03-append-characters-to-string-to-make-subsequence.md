---
title: "Leetcode Java Append Characters to String to Make Subsequence"
excerpt: "Leetcode Append Characters to String to Make Subsequence Java"
last_modified_at: 2024-06-03T18:40:00
header:
  image: /assets/images/leetcode/append-characters-to-string-to-make-subsequence.png
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
[Link](https://leetcode.com/problems/append-characters-to-string-to-make-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public int appendCharacters(String s, String t) {
    int j = 0;
    int sLength = s.length();
    int tLength = t.length();
    char[] sCharArray = s.toCharArray();
    char[] tCharArray = t.toCharArray();
    for (int i = 0; i < sLength && j < tLength; i++) {
      if (sCharArray[i] == tCharArray[j]) {
        j++;
      }
    }
    return tLength - j;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/append-characters-to-string-to-make-subsequence/submissions/1276178444/){:target="_blank"}

# 설명
1. 문자열 t를 s에 포함된 부분 문자열을 제외하고 남은 문자열의 길이을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- j는 문자열 t의 위치를 저장할 변수로, 0으로 초기화한다.
- sLength와 tLength는 s와 t의 길이를 저장한 변수이다.
- sCharArray와 tCharArray는 s와 t를 문자 배열로 변환한 변수이다.

3. 0부터 sLength 미만까지 i를 증가시키고, j가 tLength 미만일 때 까지 아래를 반복한다.
- sCharArray[i]의 문자가 tCharArray[j]의 문자와 동일한 경우, j를 증가시켜준다.

4. 반복이 완료되면 s에 순차적으로 포함된 t의 문자들을 제외한 길이인 $tLength - j$를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AppendCharactersToStringToMakeSubsequence.java){:target="_blank"}에서 확인 가능합니다.