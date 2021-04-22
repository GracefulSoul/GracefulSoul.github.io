---
title: "Leetcode Java Roman to Integer"
excerpt: "Leetcode Roman to Integer Java 풀이"
last_modified_at: 2021-04-22T18:10:00
header:
  image: /assets/images/leetcode/roman-to-integer.png
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
[Link](https://leetcode.com/problems/roman-to-integer/){:target="_blank"}

# 코드
```java
class Solution {

  public int romanToInt(String s) {
    char[] cArr = s.toCharArray();
    char lastWord = cArr[0];
    int result = getRomanValue(lastWord);
    for (int idx = 1; idx < cArr.length; idx++) {
      result += getRomanValue(cArr[idx]);
      result -= getMultipleRomanValue(new StringBuilder().append(lastWord).append(cArr[idx]).toString());
      lastWord = cArr[idx];
    }
    return result;
  }

  private int getRomanValue(char c) {
    switch (c) {
      case 'M': return 1000;
      case 'D': return 500;
      case 'C': return 100;
      case 'L': return 50;
      case 'X': return 10;
      case 'V': return 5;
      case 'I': return 1;
      default: return 0;
    }
  }

  private int getMultipleRomanValue(String s) {
    switch (s) {
      case "CM": case "CD": return 200;
      case "XC": case "XL": return 20;
      case "IX": case "IV": return 2;
      default: return 0;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/483747749/){:target="_blank"}

# 설명
1. 주어진 문자열 s를 문자 배열 cArr 변수로 변환한다.

2. 직전 문자를 저장하기 위한 lastWord에 cArr의 0번째 index 값을 저장하고, 결과를 저장하기 위한 result 변수에 해당 lastWord의 숫자로 초기화해준다.

3. 반복문을 통해서 주어진 로마 숫자 표현식을 한 단어씩 숫자로 변환한다.
  - 결과를 저장하기 위한 result 변수에 단일 로마 숫자 표현식의 숫자 값은 더하고, 복합 로마 숫자 표현식은 접두어 로마 숫자 표현식 문자의 숫자 값의 두 배를 빼준다.
  - 복합 로마 숫자 표현식의 경우 접두어 로마 숫자 표현식 문자의 숫자값의 두 배를 빼주는 이유는 단일 로마 숫자 표현식에서 이미 더했기 때문에, 그 값을 포함하여 2배를 빼주는 것이다.
  - 직전 문자를 저장하는 lastWord 변수에 해당 문자를 넣어준다.

4. 반복이 끝나면 결과를 저장한 result 변수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RomanToInteger.java){:target="_blank"}에서 확인 가능합니다.