---
title: "Leetcode Java Find the Lexicographically Largest String From the Box I"
excerpt: "Leetcode - 'Find the Lexicographically Largest String From the Box I' 문제 Java 풀이"
last_modified_at: 2025-06-04T19:10:00
header:
  image: /assets/images/leetcode/find-the-lexicographically-largest-string-from-the-box-i.png
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
[Link](https://leetcode.com/problems/find-the-lexicographically-largest-string-from-the-box-i/){:target="_blank"}

# 코드
```java
class Solution {

  public String answerString(String word, int numFriends) {
    if (numFriends == 1) {
      return word;
    } else {
      int length = word.length();
      int size = length - numFriends + 1;
      String result = "";
      String curr;
      for (int i = 0; i < length; i++) {
        curr = word.substring(i, Math.min(size + i, length));
        if (result.compareTo(curr) < 0) {
          result = curr;
        }
      }
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-lexicographically-largest-string-from-the-box-i/submissions/1653673247/){:target="_blank"}

# 설명
1. word를 재귀적으로 중복된 위치의 문제를 배제하고 numFriends 개의 비어있지 않은 문자열로 분할할 때, 분할된 문자열 중 사전적으로 가장 큰 문자열을 찾는 문제이다.

2. numFriends가 1인 하나의 문자열로 분할하는 경우, 가능한 유일한 문자열인 word를 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- length는 word의 길이를 저장한 변수이다.
- size는 분할할 문자열의 가능한 길이를 저장할 변수로, $length - numFriends + 1$로 초기화한다.
- result는 결과를 저장할 변수이고, curr은 현재 문자열을 저장할 변수이다.

4. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- curr에 word의 i번째 위치부터 $size + 1$과 length 중 작은 값 위치 미만까지 문자열을 잘라 넣어준다.
- curr이 result보다 사전적으로 큰 문자열인 경우, result에 curr을 넣어준다.

5. 반복이 완료되면 조건을 만족하는 사전적으로 가장 큰 문자열이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheLexicographicallyLargestStringFromTheBoxI.java){:target="_blank"}에서 확인 가능합니다.