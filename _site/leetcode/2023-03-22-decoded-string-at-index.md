---
title: "Leetcode Java Decoded String at Index"
excerpt: "Leetcode Decoded String at Index Java"
last_modified_at: 2023-03-22T20:00:00
header:
  image: /assets/images/leetcode/decoded-string-at-index.png
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
[Link](https://leetcode.com/problems/decoded-string-at-index){:target="_blank"}

# 코드
```java
class Solution {

  public String decodeAtIndex(String s, int k) {
    int i = 0;
    long n = 0;
    for (; n < k; i++) {
      if (Character.isDigit(s.charAt(i))) {
        n *= s.charAt(i) - '0';
      } else {
        n++;
      }
    }
    while (--i > 0) {
      if (Character.isDigit(s.charAt(i))) {
        n /= s.charAt(i) - '0';
        k %= n;
      } else {
        if (k % n == 0) {
          break;
        } else {
          n--;
        }
      }
    }
    return Character.toString(s.charAt(i));
  }

}
```

# 결과
[Link](https://leetcode.com/problems/decoded-string-at-index/submissions/920080269/){:target="_blank"}

# 설명
1. 아래의 규칙대로 만들어진 암호화된 문자열 s를 복호화 하였을 때, k번째 문자를 찾는 문제이다.
- 문자열 + 숫자의 반복으로 이루어진 s는, 앞의 문자열이 숫자만큼 반복되는 문자라는 의미이다.
- 예를 들어, "ab2cd3"를 복호화하면 "ababcdcdcd"가 된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- i는 문자열 s를 복호화 하였을 때 k번째 문자가 위치한 암호화된 문자의 위치를 저장할 변수로, 0으로 초기화한다.
- n은 k번째 문자를 탐색하기 위한 변수로, overflow를 방지하기 위해 long 형의 0으로 초기화한다.

3. n이 k 미만일 때 까지 i를 증가시키며 아래를 반복한다.
- s의 i번째 문자가 숫자인 경우, n에 n과 해당 자리의 숫자를 곱한 값을 넣어준다.
- 위의 경우가 아니라면 문자이므로, n을 증가시킨다.

4. 3번의 반복이 완료되면 i를 감소시키며 0 초과일 때까지 아래를 반복한다.
- s의 i번째 문자가 숫자인 경우, n에 n과 해당 자리의 숫자를 나눈 값을 넣어주고 k에 k와 n을 나눈 나머지 값을 넣어 반복된 문자열의 수만큼 감소시킨다.
- 위의 경우가 아니라면 k를 n으로 나눈 나머지가 0이면 위치 탐색이 완료되었으므로 반복을 중지하고, 아니면 n을 감소시킨다.

5. 반복이 완료되면 문자열 s의 i번째 문자를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DecodedStringAtIndex.java){:target="_blank"}에서 확인 가능합니다.