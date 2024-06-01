---
title: "Leetcode Java Score of a String"
excerpt: "Leetcode Score of a String Java"
last_modified_at: 2024-06-01T12:40:00
header:
  image: /assets/images/leetcode/score-of-a-string.png
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
[Link](https://leetcode.com/problems/score-of-a-string/){:target="_blank"}

# 코드
```java
class Solution {

  public int scoreOfString(String s) {
    int result = 0;
    for (int i = 0; i < s.length() - 1; i++) {
      result += Math.abs(s.charAt(i) - s.charAt(i + 1));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/score-of-a-string/submissions/1273785276/){:target="_blank"}

# 설명
1. 문자열 s의 각 문자 별 아스키 코드 값의 차이를 계산하는 문제이다.

2. result는 결과를 저장할 변수로, 0으로 초기화한다.

3. 0부터 s의 길이보다 1 작은 값까지 i를 증가시키며, s의 i번째 문자와 $i + 1$번째 문자의 아스키 코드 값의 차이에 대한 절댓값을 result에 더해준다.

4. 아스키 코드의 차잇값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ScoreOfAString.java){:target="_blank"}에서 확인 가능합니다.