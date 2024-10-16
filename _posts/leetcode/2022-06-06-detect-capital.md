---
title: "Leetcode Java Detect Capital"
excerpt: "Leetcode Detect Capital Java"
last_modified_at: 2022-06-06T12:00:00
header:
  image: /assets/images/leetcode/detect-capital.png
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
[Link](https://leetcode.com/problems/detect-capital/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean detectCapitalUse(String word) {
    int count = 0;
    for (char c : word.toCharArray()) {
      if (c - 97 < 0) {
        count++;
      }
    }
    return count == 0 ||
        word.length() == count ||
        (count == 1 && word.charAt(0) - 97 < 0);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/715381732/){:target="_blank"}

# 설명
1. word가 아래의 조건을 만족하는지 검증하는 문제이다.
- word의 모든 문자가 대문자 혹은 소문자로만 이루어져있다.
- word의 첫 문자만 대문자로 이루어져있다.

2. 대문자의 수를 저장할 count를 정의하고 word의 모든 문자를 확인하여 대문자의 수를 넣어준다.

3. 아래 조건을 확인하여 만족하는지 검증하여 하나라도 만족하면 true를, 모두 아니면 false를 주어진 문제의 결과로 반환한다.
- count가 0이면 word의 문자들이 모두 소문자로 이루어져있는 경우이다.
- word의 길이와 count가 동일하면 모두 대문자로 이루어져있는 경우이다.
- count가 1이고 word의 첫 글자가 대문자이면 첫 문자만 대문자이고 나머지는 소문자로 이루어져있는 경우이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DetectCapital.java){:target="_blank"}에서 확인 가능합니다.