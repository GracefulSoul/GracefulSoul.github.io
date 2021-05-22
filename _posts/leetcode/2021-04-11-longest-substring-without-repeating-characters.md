---
title: "Leetcode Java Longest Substring Without Repeating Characters"
excerpt: "Leetcode Longest Substring Without Repeating Characters Java 풀이"
last_modified_at: 2021-04-11T12:00:00
header:
  image: /assets/images/leetcode/longest-substring-without-repeating-characters.png
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
[Link](https://leetcode.com/problems/longest-substring-without-repeating-characters/){:target="_blank"}

# 코드
```java
class Solution {

  public int lengthOfLongestSubstring(String s) {
    int result = 0;
    Map<Character, Integer> map = new HashMap<>();
    for (int i = 0, j = 0; i < s.length(); ++i) {
      char c = s.charAt(i);
      if (map.containsKey(c)) {
        j = Math.max(j, map.get(c) + 1);
      }
      map.put(c, i);
      result = Math.max(result, i - j + 1);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/478726995/){:target="_blank"}

# 설명
1. 임시로 문자를 저장하기 위해 Collection을 선언한다.
- List가 아니라 Map을 사용하는 이유는 문자와 index를 저장하여 길이를 계산하기 위함이다.

2. 주어진 변수 s를 반복문을 통해서 고유 문자열의 길이를 계산한다.
- 변수 i는 반복문의 index로 사용한다.
- 변수 j는 반복된 문자의 index를 가져오기 위해 사용한다.

3. 주어진 변수 s의 i번째 문자를 가져와서 Collection에 존재하는지를 확인한다.
- 만일 존재한다면 반복된 문자이므로, 글자의 길이를 판단하기 위해 index + 1를 변수 j에 주입한다.
- index + 1을 사용하는 이유는 결과 값에 대한 보정치이다. (자세한건 5번에서 설명한다.)

4. Collection에 주어진 변수 s의 i번째 문자와 index를 저장한다.

5. 기존에 계산한 고유 문자열의 길이와 $i - j + 1$ 중 큰 값을 고유 문자열의 길이를 저장하는 result 변수에 주입한다.
- $i - j + 1$로 길이를 계산하는 이유는 s가 한 글자인 경우 글자의 길이가 0으로 반환되는 부분을 보정하기 위함이다.

6. 반복이 끝나면 고유 문자열의 길이를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestSubstringWithoutRepeatingCharacters.java){:target="_blank"}에서 확인 가능합니다.