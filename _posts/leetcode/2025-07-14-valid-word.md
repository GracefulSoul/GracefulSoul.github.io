---
title: "Leetcode Java Valid Word"
excerpt: "Leetcode - 'Valid Word' 문제 Java 풀이"
last_modified_at: 2025-07-15T18:30:00
header:
  image: /assets/images/leetcode/valid-word.png
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
[Link](https://leetcode.com/problems/valid-word/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isValid(String word) {
    if (word.length() < 3) {
      return false;
    } else {
      int vowels = 0;
      int consonants = 0;
      for (char c : word.toCharArray()) {
        if (Character.isLetter(c)) {
          if ("aeiouAEIOU".indexOf(c) != -1) {
            vowels++;
          } else {
            consonants++;
          }
        } else if (!Character.isDigit(c)) {
          return false;
        }
      }
      return 0 < vowels && 0 < consonants;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/valid-word/submissions/1698600446/){:target="_blank"}

# 설명
1. word의 문자열의 아래 조건을 모두 만족하는지 검증하는 문제이다.
- 최소 3자리 이상의 문자열로, 숫자와 영대소문자로만 구성되어있다.
- 영문자 모음 'a', 'e', 'i', 'o', 'u' 문자의 대소문자를 최소 하나 이상 포함한다.
- 영문자 자음 'a', 'e', 'i', 'o', 'u' 문자를 제외한 문자의 대소문자를 최소 하나 이상 포함한다.

2. word가 3자리 미만의 문자열인 경우, false를 주어진 문제의 결과로 반환한다.

3. vowels와 consonants는 모음과 자음 문자의 갯수를 저장할 변수로, 0으로 초기화한다.

4. word의 문자들을 순차적으로 c에 넣고 아래를 수행한다.
- c가 영문자이면 모음인 경우 vowels를, 자음인 경우 consonants를 증가시킨다.
- c가 영문자가 아니면 숫자가 아닌 경우, false를 주어진 문제의 결과로 반환한다.

5. 마지막으로 vowels와 consonants 모두 0보다 큰지 확인하여 해당 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidWord.java){:target="_blank"}에서 확인 가능합니다.