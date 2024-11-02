---
title: "Leetcode Java Delete Characters to Make Fancy String"
excerpt: "Leetcode - 'Delete Characters to Make Fancy String' 문제 Java 풀이"
last_modified_at: 2024-11-01T18:30:00
header:
  image: /assets/images/leetcode/delete-characters-to-make-fancy-string.png
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
[Link](https://leetcode.com/problems/delete-characters-to-make-fancy-string/){:target="_blank"}

# 코드
```java
class Solution {

  public String makeFancyString(String s) {
    char[] charArray = s.toCharArray();
    StringBuilder sb = new StringBuilder();
    int count = 1;
    for (int i = 0; i < charArray.length; i++) {
      if (0 < i && charArray[i - 1] == charArray[i]) {
        count++;
      } else {
        count = 1;
      }
      if (count < 3) {
        sb.append(charArray[i]);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/delete-characters-to-make-fancy-string/submissions/1439745394/){:target="_blank"}

# 설명
1. 문자열 s 내 동일한 문자가 연속해서 세 번 이상 발생하지 않도록 문자열을 재구성하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- sb는 동적 문자열 생성을 위한 변수로, StringBuilder로 초기화한다.
- count는 연속된 문자열의 갯수를 계산할 변수로, 1로 초기화한다.

3. 0부터 charArray의 길이 미만까지 i를 증가시키면서 아래를 반복한다.
- i가 0보다 크면서 이전 문자와 현재 문자가 동일한 경우, count를 증가시킨다.
- 위의 경우가 아니라면 count를 1로 초기화시킨다.
- 위에서 계산된 count가 3 미만인 경우, sb에 현재 문자를 넣어준다.

4. 반복이 완료되면 완성된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteCharactersToMakeFancyString.java){:target="_blank"}에서 확인 가능합니다.