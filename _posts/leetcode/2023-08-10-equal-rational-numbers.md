---
title: "Leetcode Java Equal Rational Numbers"
excerpt: "Leetcode Equal Rational Numbers Java"
last_modified_at: 2023-08-10T16:30:00
header:
  image: /assets/images/leetcode/equal-rational-numbers.png
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
[Link](https://leetcode.com/problems/equal-rational-numbers){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isRationalEqual(String s, String t) {
    return this.parse(s) == this.parse(t);
  }

  private double parse(String str) {
    int index = str.indexOf('(');
    if (index > 0) {
      StringBuilder base = new StringBuilder(str.substring(0, index));
      String num = str.substring(index + 1, str.length() - 1);
      for (int i = 1; i < 18; i++) {
        base.append(num);
      }
      return Double.valueOf(base.toString());
    } else {
      return Double.valueOf(str);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/equal-rational-numbers/submissions/1017329378/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 s와 t를 이용하여 동일한지 검증하는 문제이다.
- s의 괄호 안 문자열을 앞의 문자열에 연속해서 생성한다.

2. 문자열을 실수형으로 변환하기위한 parse(String str) 메서드를 정의한다.
- index는 str의 문자열을 자르기 위한 위치 변수로, 내 괄호 시작 문자의 위치를 찾아 넣어준다.
- index가 0보다 큰 경우 아래를 수행한다.
  - base에 str의 처음부터 index까지 문자열을 잘라 새 StringBuilder에 넣어준다.
  - num에 str의 $index + 1$번째 위치에서 마지막 이전 문자열까지 반복 숫자열을 잘라 넣어준 후 1부터 18 미만까지 i를 증가시키며 base에 num을 이어준다.
  - 반복이 완료되면 완성된 문자열인 base를 실수형으로 변환하여 반환한다.
- 위의 경우가 아니라면 정수이므로, str을 실수형으로 넣어준다.

3. 2번에서 정의한 parse(String str) 메서드를 이용하여 s와 t를 실수형으로 변환한 값이 동일한지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EqualRationalNumbers.java){:target="_blank"}에서 확인 가능합니다.