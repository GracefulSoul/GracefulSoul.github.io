---
title: "Leetcode Java To Lower Case"
excerpt: "Leetcode To Lower Case Java"
last_modified_at: 2022-10-31T18:50:00
header:
  image: /assets/images/leetcode/to-lower-case.png
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
[Link](https://leetcode.com/problems/to-lower-case){:target="_blank"}

# 코드
```java
class Solution {

  public String toLowerCase(String s) {
    char[] charArray = s.toCharArray();
    StringBuilder sb = new StringBuilder(charArray.length);
    for (char c : charArray) {
      if (c >= 'A' && c <= 'Z') {
        sb.append((char) (c + 32));
      } else {
        sb.append(c);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/833915919/){:target="_blank"}

# 설명
1. 문자열 s의 대문자를 소문자로 변환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s의 문자 배열을 변환하여 저장한 변수이다.
- sb는 동적 문자열로 결과를 저장하기 위한 변수로, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용하여 charArray의 길이의 크기로 초기화한다.

3. charArray를 반복하여 아래를 수행한다.
- c가 'A' ~ 'Z'의 대문자인 경우, 32를 더한 소문자로 변환하여 sb에 넣어준다.
- 위의 경우가 아니라면 sb에 c를 그대로 넣어준다.

4. 반복이 완료되면 소문자로 변환한 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ToLowerCase.java){:target="_blank"}에서 확인 가능합니다.