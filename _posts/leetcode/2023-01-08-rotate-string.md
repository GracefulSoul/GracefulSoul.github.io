---
title: "Leetcode Java Rotate String"
excerpt: "Leetcode - 'Rotate String' 문제 Java 풀이"
last_modified_at: 2023-01-08T09:50:00
header:
  image: /assets/images/leetcode/rotate-string.png
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
[Link](https://leetcode.com/problems/rotate-string){:target="_blank"}

# 코드
```java
class Solution {

  public boolean rotateString(String s, String goal) {
    return s.length() == goal.length() && (s + s).contains(goal);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/rotate-string/submissions/873668222/){:target="_blank"}

# 설명
1. 문자열 s의 좌측 문자열을 우측으로 이동시키며 goal의 문자열을 만들 수 있는지 검증하는 문제이다.

2. 아래의 두 조건을 만족하면 true를, 아니면 false를 주어진 문제의 결과로 반환한다.
- s의 길이와 goal의 길이가 동일한 경우.
  - 동일한 길이여야 s를 이용하여 goal로 변경이 가능하다.
- s를 두 번 반복한 문자열에 goal이 포함되는 경우.
  - s를 두 번 반복하면 좌측 문자를 우측으로 이동시키지 않아도 동일한 효과를 볼 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RotateString.java){:target="_blank"}에서 확인 가능합니다.