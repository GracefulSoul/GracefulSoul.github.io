---
title: "Leetcode Java Circular Sentence"
excerpt: "Leetcode - 'Circular Sentence' 문제 Java 풀이"
last_modified_at: 2024-11-02T19:00:00
header:
  image: /assets/images/leetcode/circular-sentence.png
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
[Link](https://leetcode.com/problems/circular-sentence/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isCircularSentence(String s) {
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    for (int i = 0; i < length; i++) {
      if (charArray[i] == ' ' && charArray[i - 1] != charArray[i + 1]) {
        return false;
      }
    }
    return charArray[0] == charArray[length - 1];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/circular-sentence/submissions/1440654079/){:target="_blank"}

# 설명
1. s의 각 띄어쓰기 단위로 문자열들을 분해해서 처음부터 마지막 문자열을 원형으로 이었을 때 이전 문자열의 마지막 문자와 다음 문자열의 처음 문자가 동일한 끝말잇기가 가능한지를 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- charArray[i]가 띄어쓰기 문자인 ' '인 경우에 그 앞뒤 문자가 동일하지 않으면 false를 주어진 문제의 결과로 반환한다.

4. charArray의 처음 문자와 마지막 문자가 동일한 마지막 문자열의 마지막 문자와 처음 문자열의 처음 문자가 다른지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CircularSentence.java){:target="_blank"}에서 확인 가능합니다.