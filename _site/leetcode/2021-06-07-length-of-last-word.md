---
title: "Leetcode Java Length of Last Word"
excerpt: "Leetcode Length of Last Word Java 풀이"
last_modified_at: 2021-06-07T12:20:00
header:
  image: /assets/images/leetcode/length-of-last-word.png
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
[Link](https://leetcode.com/problems/length-of-last-word/){:target="_blank"}

# 코드
```java
class Solution {

  public int lengthOfLastWord(String s) {
    int result = 0;
    for (int idx = s.length() - 1; idx >= 0; idx--) {
      if (s.charAt(idx) != ' ') {
        result++;
      } else {
        if (result > 0) {
          break;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/504201297/){:target="_blank"}

# 설명
1. 주어진 문자열 s의 마지막 문자열의 길이를 구하는 문제이다.

2. 주어진 문자열 s를 끝에서부터 탐색하여 문자열의 길이를 구한다.
- result의 idx번째가 ' ' 문자가 아닌 경우에는 문자열의 길이를 저장하는 result를 증가시킨다.
- result의 idx번째가 ' ' 문자인 경우, result가 0 이하면 아직 마지막 문자열이 시작되지 않았으므로 무시한다.
- result의 idx번째가 ' ' 문자인 경우, result가 0 보다 크면 반복문을 종료한다.

3. 반복문이 종료되면 마지막 문자열의 길이를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LengthOfLastWord.java){:target="_blank"}에서 확인 가능합니다.