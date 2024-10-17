---
title: "Leetcode Java Word Pattern"
excerpt: "Leetcode - 'Word Pattern' 문제 Java 풀이"
last_modified_at: 2021-12-08T09:00:00
header:
  image: /assets/images/leetcode/word-pattern.png
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
[Link](https://leetcode.com/problems/word-pattern/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean wordPattern(String pattern, String s) {
    char[] patterns = pattern.toCharArray();
    String[] words = s.split(" ");
    if (patterns.length != words.length) {
      return false;
    }
    Map<Object, Integer> map = new HashMap<>();
    for (Integer idx = 0; idx < words.length; idx++) {
      if (map.put(patterns[idx], idx) != map.put(words[idx], idx)) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/598577015/){:target="_blank"}

# 설명
1. 주어진 문자열 s의 문자 조합이 동일한 문자열 pattern의 형태와 유사한지를 검증하는 문제이다.
- 예를 들어, pattern이 "abc"이면 s는 "attachement file folder"로 각자 다른 단어로 구성되어야 한다.
- 예제를 보아, pattern이 "abc"일때 s는 "file folder file"로 a와 c가 동일해서는 안 된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- patterns는 pattern을 각 문자 단위로 나누어 저장한 문자 배열이다.
- words는 s를 공백(" ")으로 구분한 단어들의 문자열 배열이다.

3. patterns와 words의 길이가 같지 않는다면 기본 형태가 다르므로, false를 주어진 문제의 결과로 반환한다.

4. patterns와 words의 요소들을 각각 임시 저장할 map을 정의한다.

5. patterns와 words를 모두 탐색한다.
- map에 patterns의 idx번째 요소와 words의 idx번째 요소를 각각 idx 값으로 넣어주고 각 값이 idx가 아니면 두 개의 pattern에 word가 동일하게 들어간 경우이므로, false를 주어진 문제의 결과로 반환한다.

6. 반복이 종료되면 patterns의 요소들에 words의 각 요소들이 알맞은 패턴으로 구성되었다는 의미이므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WordPattern.java){:target="_blank"}에서 확인 가능합니다.