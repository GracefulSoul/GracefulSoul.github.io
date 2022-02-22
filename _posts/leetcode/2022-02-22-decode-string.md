---
title: "Leetcode Java Decode String"
excerpt: "Leetcode Decode String Java 풀이"
last_modified_at: 2022-02-22T18:00:00
header:
  image: /assets/images/leetcode/decode-string.png
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
[Link](https://leetcode.com/problems/decode-string/){:target="_blank"}

# 코드
```java
class Solution {

  private int index = 0;

  public String decodeString(String s) {
    StringBuilder result = new StringBuilder();
    while (index < s.length() && s.charAt(index) != ']') {
      if (Character.isDigit(s.charAt(index))) {
        int repeat = 0;
        while (Character.isDigit(s.charAt(index))) {
          repeat = (repeat * 10) + (s.charAt(index++) - '0');
        }
        index++;
        String word = this.decodeString(s);
        for (int idx = 0; idx < repeat; idx++) {
          result.append(word);
        }
        index++;
      } else {
        result.append(s.charAt(index++));
      }
    }
    return result.toString();
  }


}
```

# 결과
[Link](https://leetcode.com/submissions/detail/646649651/){:target="_blank"}

# 설명
1. 주어진 문자열 s를 이용하여 아래의 규칙대로 수행한 결과를 반환하는 문제이다.
- k[encoded_string]로 표기된 문자열은 encoded_string을 k번 반복하면 된다.
- encoded_string 내 k[encoded_string]로 표기된 문자열은 안쪽부터 먼저 변환 후 바깥쪽에서 변환한다.

2. index는 주어진 문자열의 위치를 나타내며, 0으로 초기화한다.
- decodeString(String s)를 재귀 호출하여 전역 변수를 정의한다.

3. result는 결과를 저장할 StringBuilder 객체이다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

4. index가 s의 길이보다 작고, index번째 문자가 ']'가 아닐 때 까지 반복을 수행한다.
- s의 index번째 문자가 숫자인 경우, 아래를 수행한다.
  - 반복 횟수를 넣을 repeat를 0으로 초기화하고, 숫자인 값을 repeat에 넣어준다.
  - 숫자를 넣은 다음 값은 '[' 문자이므로, index를 증가시킨다.
  - word는 재귀 호출을 이용하여 다음 ']'문자까지 값을 받아 초기화한다.
  - 0부터 repeat 전까지 반복하여 result에 word를 repeat번 넣어준다.
  - 값을 다 넣은 다음 값은 ']'이므로, index를 증가시킨다.
- s의 index번째 문자가 숫자가 아닌 경우 단순 문자열이므로, result에 s의 index번째 문자를 넣고 index를 증가시킨다.

5. 반복이 완료되면 result를 문자열로 변환시켜 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DecodeString.java){:target="_blank"}에서 확인 가능합니다.