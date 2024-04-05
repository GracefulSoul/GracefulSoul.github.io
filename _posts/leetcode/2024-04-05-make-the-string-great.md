---
title: "Leetcode Java Make The String Great"
excerpt: "Leetcode Make The String Great Java"
last_modified_at: 2024-04-05T18:30:00
header:
  image: /assets/images/leetcode/make-the-string-great.png
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
[Link](https://leetcode.com/problems/make-the-string-great/){:target="_blank"}

# 코드
```java
class Solution {

  public String makeGood(String s) {
    for (int i = 0; i < s.length() - 1; i++) {
      if (Math.abs(s.charAt(i) - s.charAt(i + 1)) == 32) {
        return this.makeGood(s.substring(0, i) + s.substring(i + 2));
      }
    }
    return s;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/submissions/1222934960/){:target="_blank"}

# 설명
1. 문자열 s를 아래의 조건을 만족하는 좋은 문자열을 만들어 반환하는 문제이다.
- i는 [0, $s.length - 2$] 사이의 값이다.
- s의 i번째 문자가 영소문자일 때 $i + 1$번째 문자가 동일한 영대문자이거나 그 반대의 경우를 만족하면 제거한다.
- 제거 후 위의 절차를 반복 수행하여 제거할 문자가 존재하지 않는 문자열이다.

2. 0부터 $s.length - 1$까지 i를 증가시키며 아래를 반복한다.
- s의 i번째 문자와 $i + 1$번째 문자가 동일한 문자의 대/소문자인 경우, 앞의 두 문자를 제거한 문자열로 재귀 호출을 수행한 결과를 반환한다.

3. 위의 결과가 존재하지 않으면 제거할 문자들이 없으므로, s를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MakeTheStringGreat.java){:target="_blank"}에서 확인 가능합니다.