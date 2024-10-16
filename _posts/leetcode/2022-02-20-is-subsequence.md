---
title: "Leetcode Java Is Subsequence"
excerpt: "Leetcode Is Subsequence Java 풀이"
last_modified_at: 2022-02-20T15:00:00
header:
  image: /assets/images/leetcode/is-subsequence.png
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
[Link](https://leetcode.com/problems/is-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isSubsequence(String s, String t) {
    int index = -1;
    for (int idx = 0; idx < s.length(); idx++) {
      index = t.indexOf(s.charAt(idx), index + 1);
      if (index == -1) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/645042562/){:target="_blank"}

# 설명
1. 주어진 문자열 s가 t의 부분 문자들로 이루어졌는지를 검증하는 문제이다.
- 단 s와 t의 문자들의 순서는 차례대로 유지되어야 한다.
- 예를 들어, t가 "asbdc"이면 s가 "abc"이면 true이고 "acb"이면 false가 된다.

2. 문자의 위치를 저장하기 위한 index를 -1로 정의한다.

3. 0부터 s의 길이만큼 idx를 증가시키며 반복하여 검증을 수행한다.
- index에 t에서 $index + 1$번째 이후 문자들 중 s의 idx번째 문자의 위치 값을 넣어준다.
- 위의 검증에서 해당 문자가 없어 index가 -1인 경우, false를 주어진 문제의 결과로 반환한다.
- 그렇지 않은 경우, 반복을 계속 수행한다.

4. 반복이 완료되면 s가 t의 부분 문자들로 이루어져 있으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IsSubsequence.java){:target="_blank"}에서 확인 가능합니다.