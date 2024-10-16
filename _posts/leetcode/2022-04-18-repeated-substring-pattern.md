---
title: "Leetcode Java Repeated Substring Pattern"
excerpt: "Leetcode Repeated Substring Pattern Java 풀이"
last_modified_at: 2022-04-18T13:00:00
header:
  image: /assets/images/leetcode/repeated-substring-pattern.png
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
[Link](https://leetcode.com/problems/repeated-substring-pattern/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean repeatedSubstringPattern(String s) {
    int length = s.length();
    for (int index = 1; index <= length / 2; index++) {
      if (length % index == 0) {
        String pattern = s.substring(0, index);
        boolean isRepeated = true;
        for (int curr = length - index; curr > 0; curr -= index) {
          if (!pattern.equals(s.substring(curr, curr + index))) {
            isRepeated = false;
            break;
          }
        }
        if (isRepeated) {
          return true;
        }
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/682513546/){:target="_blank"}

# 설명
1. 문자열 s가 반복된 문자열로 이루어져 있는지 검증하는 문제이다.

2. length s의 길이를 에 저장할 변수로, s의 길이로 초기화한다.

3. 반복되는 문자열의 최대 길이는 해당 문자열의 절반이므로, 1부터 $\frac{length}{2}$ 이하까지 index를 증가시키며 아래를 반복한다.
- length를 index로 나눈 나머지가 0이 아니면 다음 반복을 진행한다.
- pattern에 s의 처음부터 index번째 자리 이전까지 잘라 반복이 되는 패턴으로 저장한다.
- isRepeated를 true로 초기화한다.
- curr를 $length - index$부터 0초과까지 curr를 index만큼 감소시키며 아래의 반복을 수행한다.
  - pattern이 s의 curr번째 자리부터 $curr + index$ 번째 자리 이전까지 잘라 동일한지 검증하여, 동일하지 않은 경우 isRepeated를 false로 변경하고 반복을 종료한다.
- 반복이 완료되고 isRepeated가 true인 경우 반복이 성립되므로, true를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RepeatedSubstringPattern.java){:target="_blank"}에서 확인 가능합니다.