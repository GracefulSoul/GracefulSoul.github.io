---
title: "Leetcode Java Check If Word Is Valid After Substitutions"
excerpt: "Leetcode Check If Word Is Valid After Substitutions Java"
last_modified_at: 2023-10-16T19:45:00
header:
  image: /assets/images/leetcode/check-if-word-is-valid-after-substitutions.png
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
[Link](https://leetcode.com/problems/check-if-word-is-valid-after-substitutions){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isValid(String s) {
    String abc = "abc";
    while (s.contains(abc)) {
      s = s.replace(abc, "");
    }
    return s.isEmpty();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-word-is-valid-after-substitutions/submissions/1076584965/){:target="_blank"}

# 설명
1. "abc" 문자열을 이용하여 문자열 s를 만들 수 있는지 검증하는 문제이다.

2. s 문자열에서 "abc" 문자열이 존재하면 하나 씩 제거한 후, 빈 문자열인지 검증한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfWordIsValidAfterSubstitutions.java){:target="_blank"}에서 확인 가능합니다.