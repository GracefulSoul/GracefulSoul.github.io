---
title: "Leetcode Java Repeated String Match"
excerpt: "Leetcode Repeated String Match Java"
last_modified_at: 2022-10-07T19:50:00
header:
  image: /assets/images/leetcode/repeated-string-match.png
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
[Link](https://leetcode.com/problems/repeated-string-match){:target="_blank"}

# 코드
```java
class Solution {

  public int repeatedStringMatch(String a, String b) {
    StringBuilder sb = new StringBuilder(a);
    int count = 1;
    while (sb.indexOf(b) == -1) {
      if (sb.length() - a.length() > b.length()) {
        return -1;
      }
      sb.append(a);
      count++;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/817130482/){:target="_blank"}

# 설명
1. b가 존재하기 위한 a의 반복 횟수를 구하는 문제이다.
- "abc"를 0번 반복된 문자열은 ""이며, 1번 반복된 문자열은 "abc", 2번 반복된 문자열은 "abcabc"이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 동적으로 문자열을 이어줄 변수로, a를 넣어 초기화한다.
- count는 반복 횟수를 저장할 변수로, 1로 초기화한다.

3. sb에서 b가 존재하지 않을 때 까지 아래를 반복한다.
- sb의 길이에서 a의 길이를 뺀 값이 b의 길이보다 큰 경우 이미 존재하지 않는 결과이므로, -1을 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니라면 sb에 a 문자열을 이어주고, count를 증가시킨다.

4. 반복이 완료되면 반복 횟수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RepeatedStringMatch.java){:target="_blank"}에서 확인 가능합니다.