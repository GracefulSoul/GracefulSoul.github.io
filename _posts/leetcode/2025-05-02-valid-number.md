---
title: "Leetcode Java Valid Number"
excerpt: "Leetcode - 'Valid Number' 문제 Java 풀이"
last_modified_at: 2025-05-02T18:40:00
header:
  image: /assets/images/leetcode/valid-number.png
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
[Link](https://leetcode.com/problems/valid-number/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isNumber(String s) {
    char[] charArray = s.toCharArray();
    boolean seenNumber = false;
    boolean seenExponent = false;
    boolean seenDot = false;
    for (int i = 0; i < charArray.length; i++) {
      switch (charArray[i]) {
        case '.':
          if (seenDot || seenExponent) {
            return false;
          } else {
            seenDot = true;
            break;
          }
        case 'e': case 'E':
          if (seenExponent || !seenNumber) {
            return false;
          } else {
            seenExponent = true;
            seenNumber = false;
            break;
          }
        case '+': case '-':
          if (i != 0 && (charArray[i - 1] != 'e' && charArray[i - 1] != 'E')) {
            return false;
          } else {
            seenNumber = false;
            break;
          }
        default:
          if (charArray[i] - '0' < 0 || charArray[i] - '0' > 9) {
            return false;
          } else {
            seenNumber = true;
          }
      }
    }
    return seenNumber;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/valid-number/submissions/1623502311/){:target="_blank"}

# 설명
1. 문자열 s가 숫자로 표시 가능한지 검증하는 문제이다.
- 숫자는 정수 혹은 실수로 표현된다.
- '+', '-' 부호가 포함될 수 있다.
- 지수 표현인 'e', 'E' 문자가 포함될 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 문자열 s를 문자 배열로 변환한 변수이다.
- seenNumber는 숫자를 마주친 경우를 저장할 변수로, false로 초기화한다.
- seenExponent는 지수를 마주친 경우를 저장할 변수로, false로 초기화한다.
- seenDot는 실수의 소수점 표시를 마주친 경우 저장할 변수로, false로 초기화한다.

3. 0부터 charArray의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- charArray[i]의 값에 따라서 아래를 수행한다.
  - '.' 문자인 경우, seenDot 혹은 seenExponent의 값이 true이면 false를 반환하고 아니면 seenDot을 true로 바꾸고 다음 반복을 수행한다.
  - 'e' 혹은 'E' 문자인 경우, seenExponent의 값이 true이거나 seenNumber의 값이 false이면 false를 반환하고 아니면 seenExponent 값에 true를 seenNumber의 값에 false를 넣어준다.
  - '+' 혹은 '-' 문자인 경우, i가 0이 아니면서 이전 문자가 'e' 혹은 'E'가 아니면 false를 반환하고 아니면 seenNumber를 false로 바꿔준다.
  - 그 외로 charArray[i]의 값이 [0, 9] 사이의 숫자가 아니면 false를 반환하고 아니면 seenNumber를 true로 바꿔준다.

4. 반복이 완료되면 seenNumber의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidNumber.java){:target="_blank"}에서 확인 가능합니다.