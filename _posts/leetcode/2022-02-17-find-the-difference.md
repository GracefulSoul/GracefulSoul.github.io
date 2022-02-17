---
title: "Leetcode Java Find the Difference"
excerpt: "Leetcode Find the Difference Java 풀이"
last_modified_at: 2022-02-17T12:00:00
header:
  image: /assets/images/leetcode/find-the-difference.png
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
[Link](https://leetcode.com/problems/find-the-difference/){:target="_blank"}

# 코드
```java
class Solution {

  public char findTheDifference(String s, String t) {
    char[] sCharArray = s.toCharArray();
    char[] tCharArray = t.toCharArray();
    int diff = 0;
    for (int idx = 0; idx < sCharArray.length; idx++) {
      diff += tCharArray[idx] - sCharArray[idx];
    }
    return (char) (diff + tCharArray[sCharArray.length]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/642948325/){:target="_blank"}

# 설명
1. 주어진 문자열 t에서 s에서 누락된 문자를 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sCharArray는 주어진 문자열 s를 문자 배열로 변환하여 사용할 변수이다.
- tCharArray는 주어진 문자열 t를 문자 배열로 변환하여 사용할 변수이다.
- diff는 주어진 문자열 s와 t의 차이를 담을 변수이다.

3. 주어진 문자열 t는 s보다 한 글자 많기 때문에 0부터 sCharArray의 길이만큼 idx를 증가시키며 반복시킨다.
- diff에 tCharArray 배열 내 idx번째 문자의 정수형과 sCharArray 배열 내 idx번째 문자의 정수형의 차이를 넣어주고 반복을 계속 수행한다.

4. diff에 tCharArray의 마지막 문자를 더해서 문자로 변환한 값을 주어진 문자로 반환한다.
- tCharArray 배열 내 문자들의 ASCII Code 값의 합에 sCharArray 배열 내 문자들의 ASCII Code의 합을 뺀 경우, sCharArray에 누락된 문자의 ASCII 코드 값이 나와 문자로 변환하면 해당 영문자로 반환이 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestAbsoluteFilePath.java){:target="_blank"}에서 확인 가능합니다.