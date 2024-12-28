---
title: "Leetcode Java Split a String in Balanced Strings"
excerpt: "Leetcode - 'Split a String in Balanced Strings' 문제 Java 풀이"
last_modified_at: 2024-12-28T11:20:00
header:
  image: /assets/images/leetcode/split-a-string-in-balanced-strings.png
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
[Link](https://leetcode.com/problems/split-a-string-in-balanced-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public int balancedStringSplit(String s) {
    int result = 0;
    int count = 0;
    for (char c : s.toCharArray()) {
      if (c == 'L') {
        count++;
      } else {
        count--;
      }
      if (count == 0) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/split-a-string-in-balanced-strings/submissions/1490263373/){:target="_blank"}

# 설명
1. 'L'과 'R' 문자로 이루어진 문자열 s를 각 문자의 갯수가 동일하게 부분 문자열로 분리할 수 있는 최대 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 부분 문자열의 최대 갯수를 저장할 변수로, 0으로 초기화한다.
- count는 'L' 문자와 'R' 문자 갯수 차이를 저장할 변수로, 0으로 초기화한다.

3. s의 문자를 순차적으로 c에 넣어 아래를 수행한다.
- c가 'L'인 경우 count를 증가시키고, 'R'인 경우 count를 감소시킨다.
- count가 0인 문자 갯수가 동일한 위치인 경우, result를 증가시켜준다.

4. 반복이 완료되면 부분 문자열의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SplitAStringInBalancedStrings.java){:target="_blank"}에서 확인 가능합니다.