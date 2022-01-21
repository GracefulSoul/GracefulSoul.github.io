---
title: "Leetcode Java Reverse Vowels of a String"
excerpt: "Leetcode Reverse Vowels of a String Java 풀이"
last_modified_at: 2022-01-20T20:00:00
header:
  image: /assets/images/leetcode/reverse-vowels-of-a-string.png
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
[Link](https://leetcode.com/problems/reverse-vowels-of-a-string/){:target="_blank"}

# 코드
```java
class Solution {

  public String reverseVowels(String s) {
    char[] charArray = s.toCharArray();
    int start = 0;
    int end = s.length() - 1;
    while (start < end) {
      while (this.isConsonant(charArray[start])) {
        if (start >= end) {
          break;
        }
        start++;
      }
      while (this.isConsonant(charArray[end]) && start < end) {
        if (start >= end) {
          break;
        }
        end--;
      }
      char temp = charArray[start];
      charArray[start] = charArray[end];
      charArray[end] = temp;
      start++;
      end--;
    }
    return new String(charArray);
  }

  private boolean isConsonant(char c) {
    return !(c == 'A' || c == 'a' ||
         c == 'E' || c == 'e' ||
         c == 'I' || c == 'i' ||
         c == 'O' || c == 'o' ||
         c == 'U' || c == 'u');
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/624590953/){:target="_blank"}

# 설명
1. 주어진 문자열 s의 모음 단어('a', 'e', 'i', 'o' , 'u')의 순서를 반전시키고 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 주어진 문자열 s를 문자 배열로 변환해서 저장할 변수이다.
- start는 문자열 s의 좌측부터 탐색할 변수로, 0으로 초기화한다.
- end는 문자열 s의 우측부터 탐색할 변수로, $s.length - 1$로 초기화 한다. 

3. start가 end보다 작을 때 까지 반복하여 문자열의 순서를 변경한다.
- charArray에서 start번째 문자가 모음 단어일 때 까지 반복을 수행하여 start가 end보다 큰 경우 반복을 그만하고, 그렇지 않으면 start를 증가시킨다.
- charArray에서 end번째 문자가 모음 단어이고 start가 end보다 작을 때 까지 반복을 수행하여 start가 end보다 큰 경우 반복을 그만하고, 그렇지 않으면 end를 감소시킨다.
- 위에서 결정된 start와 end 자리의 문자를 교체해주고, start는 증가시키고 end는 감소시킨 후 반복을 계속 수행한다.

4. 반복이 완료되면 charArray를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseVowelsOfAString.java){:target="_blank"}에서 확인 가능합니다.