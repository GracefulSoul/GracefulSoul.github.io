---
title: "Leetcode Java String Without AAA or BBB"
excerpt: "Leetcode Medium - 'String Without AAA or BBB' 문제 Java 풀이"
last_modified_at: 2023-09-01T18:40:00
header:
  image: /assets/images/leetcode/string-without-aaa-or-bbb.png
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
[Link](https://leetcode.com/problems/string-without-aaa-or-bbb){:target="_blank"}

# 코드
```java
class Solution {

  public String strWithout3a3b(int a, int b) {
    StringBuilder sb = new StringBuilder(a + b);
    char ca = 'a';
    char cb = 'b';
    if (b > a) {
      ca = 'b';
      cb = 'a';
      int temp = a;
      a = b;
      b = temp;
    }
    while (a-- > 0) {
      sb.append(ca);
      if (a > b) {
        sb.append(ca);
        a--;
      }
      if (b-- > 0) {
        sb.append(cb);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/string-without-aaa-or-bbb/submissions/1037528879/){:target="_blank"}

# 설명
1. a와 b를 아래의 규칙대로 수행한 문자열로 반환하는 문제이다.
- 문자열의 길이는 $a + b$이며, a는 'a'문자 b는 'b' 문자를 의미한다.
- 'aaa', 'bbb'와 같은 세 번 연속된 문자열은 s에 존재하지 않는다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 결과 문자열을 동적으로 만들기 위한 변수로, $a + b$ 크기의 StringBuilder로 정의한다.
- ca와 cb는 a와 b를 문자열로 저장한 변수로, a와 b를 넣고 b가 a보다 큰 경우 a와 b, ca와 cb의 값을 바꿔준다.

3. a가 0보다 큰 경우 아래를 수행하고 a를 감소시킨다.
- sb에 ca를 넣고 a가 b보다 큰 경우, sb에 ca를 이어주고 a를 감소시킨다.
- b가 0보다 큰 경우, sb에 cb를 넣어 a가 3번 연속되는걸 방지해준다.
- b를 감소시켜 b의 수를 감소시킨다.

4. 반복이 완료되어 완성된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StringWithoutAAAOrBBB.java){:target="_blank"}에서 확인 가능합니다.