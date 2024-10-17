---
title: "Leetcode Java Isomorphic Strings"
excerpt: "Leetcode - 'Isomorphic Strings' 문제 Java 풀이"
last_modified_at: 2021-10-10T12:00:00
header:
  image: /assets/images/leetcode/isomorphic-strings.png
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
[Link](https://leetcode.com/problems/isomorphic-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isIsomorphic(String s, String t) {
    int[] sm = new int[256];
    int[] tm = new int[256];
    for (int i = 0; i < s.length(); i++) {
      if (sm[s.charAt(i)] != tm[t.charAt(i)]) {
        return false;
      } else {
        sm[s.charAt(i)] = tm[t.charAt(i)] = i + 1;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/568702775/){:target="_blank"}

# 설명
1. 주어진 문자열 s와 t가 동일한 형태의 문자열인지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sm과 tm은 각 문자열이 동일한 형태인 문자열인지 검증하기 위한 배열로, ASCII 코드의 문자수인 256으로 설정한다.

3. 주어진 문자열 s와 t를 반복하여 동일한 형태의 문자열인지 검증한다.
- sm 배열 내 s의 i번째 문자의 ASCII 코드 번호에 위치한 값과 tm 배열 내 t의 i번째 문자의 ASCII 코드 번호에 위치한 값이 동일하지 않으면 동일한 형태의 문자열이 아니므로, false를 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니면 sm 배열 내 s의 i번째 문자의 ASCII 코드 번호에 위치한 값과 tm 배열 내 t의 i번째 문자의 ASCII 코드 번호에 위치한 값에 $i + 1$을 넣어 동일하게 발생한 위치를 저장한다.

4. 반복이 완료되면 주어진 문자열 s와 t가 동일한 형태의 문자열이므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IsomorphicStrings.java){:target="_blank"}에서 확인 가능합니다.