---
title: "Leetcode Java String Compression III"
excerpt: "Leetcode - 'String Compression III' 문제 Java 풀이"
last_modified_at: 2024-11-04T18:00:00
header:
  image: /assets/images/leetcode/string-compression-iii.png
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
[Link](https://leetcode.com/problems/string-compression-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public String compressedString(String word) {
    StringBuilder sb = new StringBuilder();
    int count = 1;
    char c = word.charAt(0);
    for (int i = 1; i < word.length(); i++) {
      if (c == word.charAt(i) && count < 9) {
        count++;
      } else {
        sb.append(count).append(c);
        c = word.charAt(i);
        count = 1;
      }
    }
    return sb.append(count).append(c).toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/string-compression-iii/submissions/1442575588/){:target="_blank"}

# 설명
1. word의 각 문자들을 반복 횟수 + 문자 형태로 변환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 동적 문자열 생성에 필요한 변수로, StringBuilder로 초기화한다.
- count는 문자의 갯수를 계산할 변수로, 1로 초기화한다.
- c는 반복되는 문자를 임시 저장할 변수로, word의 첫 문자로 초기화한다.

3. 1부터 word의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- c와 word의 i번째 문자가 동일한 경우, count를 증가시킨다.
- c와 word의 i번째 문자가 다른 경우, 아래를 수행한다.
  - sb에 count와 c를 순차적으로 넣어준다.
  - c에 word의 i번째 문자를 넣고, count를 1로 초기화한다.

4. 반복이 완료되면 마지막으로 sb에 count와 c를 다시 넣어준 후 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StringCompressionIII.java){:target="_blank"}에서 확인 가능합니다.