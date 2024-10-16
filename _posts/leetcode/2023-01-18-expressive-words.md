---
title: "Leetcode Java Expressive Words"
excerpt: "Leetcode Expressive Words Java"
last_modified_at: 2023-01-18T19:40:00
header:
  image: /assets/images/leetcode/expressive-words.png
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
[Link](https://leetcode.com/problems/expressive-words){:target="_blank"}

# 코드
```java
class Solution {

  public int expressiveWords(String s, String[] words) {
    int result = 0;
    for (String word : words) {
      if (this.isPossible(s.toCharArray(), word.toCharArray())) {
        result++;
      }
    }
    return result;
  }

  private boolean isPossible(char[] sCharArray, char[] wordCharArray) {
    int sLength = sCharArray.length;
    int wordLength = wordCharArray.length;
    int j = 0;
    for (int i = 0; i < sLength; i++) {
      if (j < wordLength && sCharArray[i] == wordCharArray[j]) {
        j++;
      } else if (!(0 < i && i < sLength - 1 && sCharArray[i - 1] == sCharArray[i] && sCharArray[i] == sCharArray[i + 1])
          && !(1 < i && sCharArray[i - 2] == sCharArray[i - 1] && sCharArray[i - 1] == sCharArray[i])) {
        return false;
      }
    }
    return j == wordLength;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/expressive-words/submissions/880490942/){:target="_blank"}

# 설명
1. words의 문자들 중 s로 확장 가능한 문자열의 수를 구하는 문제이다.
- 확장은 동일한 문자가 3번 이상 반복되도록만 확장이 가능하다.

2. result는 확장 가능한 문자열의 수를 저장하기 위한 변수로, 0으로 초기화한다.

3. words의 모든 문자열을 word에 넣어 아래를 반복한다.
- 4번에서 정의한 isPossible(char[] sCharArray, char[] wordCharArray) 메서드를 s와 word 모두 문자 배열로 변환하여 수행한 결과가 true이면 result를 증가시킨다.

4. 문자열 word가 문자열 s로 확장 가능한지를 검증하기 위한 isPossible(char[] sCharArray, char[] wordCharArray) 메서드를 정의한다.
- 검증을 위한 변수를 정의한다.
  - sLength와 wordLength는 s와 word의 길이를 저장한 변수이다.
  - j는 wordCharArray를 탐색하기 위한 위치 변수로, 0으로 초기화한다.
- 0부터 sLength 미만까지 i를 증가시키며 아래를 검증한다.
- j가 wordLength 미만이면서 sCharArray의 i번째 문자와 wordCharArray의 j번째 문자가 동일하면 j를 증가시키고 반복을 계속한다.
- 위의 경우가 아니고 아래를 동일 문자가 세 번 반복된 경우를 만족하지 않으면 확장이 불가능하므로, false를 반환한다.
  - i가 0 초과이면서 $sLength - 1$ 미만인 경우, sCharArray의 i번째 문자의 이전 문자와 이후 문자 모두 동일한 경우.
  - i가 1 초과인 경우, sCharArray의 $i - 1$번째 문자의 이전 문자와 이후 문자 모두 동일한 경우.
- 반복이 완료되면 j가 wordLegnth와 동일한 마지막 위치인지 검증하여 확장 가능한지 여부를 반환한다.

5. 3번의 반복이 완료되면 확장 가능한 문자열의 수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ExpressiveWords.java){:target="_blank"}에서 확인 가능합니다.