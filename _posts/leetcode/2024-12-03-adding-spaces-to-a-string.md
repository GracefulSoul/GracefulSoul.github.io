---
title: "Leetcode Java Adding Spaces to a String"
excerpt: "Leetcode - 'Adding Spaces to a String' 문제 Java 풀이"
last_modified_at: 2024-12-03T19:40:00
header:
  image: /assets/images/leetcode/adding-spaces-to-a-string.png
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
[Link](https://leetcode.com/problems/adding-spaces-to-a-string/){:target="_blank"}

# 코드
```java
class Solution {

  public String addSpaces(String s, int[] spaces) {
    StringBuilder sb = new StringBuilder();
    char[] charArray = s.toCharArray();
    int i = 0;
    for (int space : spaces) {
      while (i < space) {
        sb.append(charArray[i++]);
      }
      sb.append(' ');
    }
    while (i < charArray.length) {
      sb.append(charArray[i++]);
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/adding-spaces-to-a-string/submissions/1469153846/){:target="_blank"}

# 설명
1. 문자열 s에서 각 spaces의 값들의 위치에 띄어쓰기(" ")를 추가하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 동적인 문자열 생성에 필요한 변수로, StringBuilder로 초기화한다.
- charArray는 문자열 s를 문자 배열로 변환한 변수이다.
- i는 문자열 위치를 저장할 변수로, 0으로 초기화한다.

3. spaces의 각 값을 space에 순차적으로 넣어 아래를 수행한다.
- i가 space 미만일 때 까지 sb에 charArray[i] 문자를 넣어준 후 i를 증가시켜준다.
- 반복이 완료되면 sb에 띄어쓰기(" ")를 추가한다.

4. 공백이 모두 추가되면 i가 charArray의 길이 미만까지 sb에 나머지 문자를 넣어준다.

5. 모든 반복이 완료되어 완성된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AddingSpacesToAString.java){:target="_blank"}에서 확인 가능합니다.