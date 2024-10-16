---
title: "Leetcode Java First Unique Character in a String"
excerpt: "Leetcode First Unique Character in a String Java 풀이"
last_modified_at: 2022-02-15T17:00:00
header:
  image: /assets/images/leetcode/first-unique-character-in-a-string.png
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
[Link](https://leetcode.com/problems/first-unique-character-in-a-string/){:target="_blank"}

# 코드
```java
class Solution {

  public int firstUniqChar(String s) {
    int index = Integer.MAX_VALUE;
    for (char c = 'a'; c <= 'z'; c++) {
      int first = s.indexOf(c);
      if (first != -1 && first == s.lastIndexOf(c)) {
        index = Math.min(index, first);
      }
    }
    return index == Integer.MAX_VALUE ? -1 : index;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/641758858/){:target="_blank"}

# 설명
1. 주어진 문자열 s 내 단 한번만 사용된 최초 문자를 찾아 해당 위치를 반환하는 문제이다.

2. 문자열 s 내 유일한 문자의 위치를 index에 정수의 가장 큰 값을 넣어 초기화 한다.

3. 'a' 문자부터 'z'까지 c를 반복하며 문자열 s를 탐색한다.
- 해당 문자의 위치가 -1이 아니면서 처음과 마지막의 위치가 동일한 경우 문자열 s 내 유일한 문자이므로, index에 index와 해당 문자의 위치인 first 중 작은(앞의 위치에 해당하는) 값을 넣어준다.

4. index가 초기 값인 정수의 최대 값인지를 확인하여 경우에 따라 주어진 문제의 결과를 반환한다.
- index가 초기 값 그대로인 경우 유일한 문자가 존재하지 않는다는 의미이므로, -1을 주어진 문제의 결과로 반환한다.
- 위의 경우가 아닌 경우 유일한 문자가 최소 1개 이상 존재하므로, 가장 먼저 존재하는 문자의 위치를 저장한 index를 주어진 문제의 결과로 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FirstUniqueCharacterInAString.java){:target="_blank"}에서 확인 가능합니다.