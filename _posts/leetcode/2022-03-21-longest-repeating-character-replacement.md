---
title: "Leetcode Java Longest Repeating Character Replacement"
excerpt: "Leetcode Longest Repeating Character Replacement Java 풀이"
last_modified_at: 2022-03-21T13:00:00
header:
  image: /assets/images/leetcode/longest-repeating-character-replacement.png
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
[Link](https://leetcode.com/problems/longest-repeating-character-replacement/){:target="_blank"}

# 코드
```java
class Solution {

  public int characterReplacement(String s, int k) {
    int[] chars = new int[26];
    int max = 0;
    int maxLength = 0;
    int start = 0;
    int length = s.length();
    char[] charArray = s.toCharArray();
    for (int idx = 0; idx < length; idx++) {
      int num = charArray[idx] - 'A';
      chars[num]++;
      if (chars[num] > max) {
        max = chars[num];
      }
      while (idx - start + 1 > max + k) {
        chars[charArray[start] - 'A']--;
        start++;
      }
      maxLength = Math.max(maxLength, idx - start + 1);
    }
    return maxLength;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/664142100/){:target="_blank"}

# 설명
1. 문자열 s가 주어지면 k개의 문자를 변환하여 동일한 알파벳을 최대 몇 개까지 연속해서 구성할 수 있는지 탐색하는 문제이다.
- 단, 모든 문자는 영 대문자로 이루어져있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- chars는 알파벳을 임시 저장하기 위한 변수로, 영문자의 갯수인 26의 크기로 초기화한다.
- max는 해당 영문자의 갯수를 저장할 변수로, 0으로 초기화한다.
- maxLength는 동일한 영문자로 구성한 최대 길이를 저장할 변수로, 0으로 초기화한다.
- start는 동일 영문자로 구성하기 위한 시작 위치를 저장할 변수로, 0으로 초기화한다.
- length는 문자열 s의 길이를 저장할 변수로, s의 길이로 초기화한다.
- charArray는 문자열 s를 문자 배열로 변환하여 저장할 변수로, s를 문자의 배열로 변환하여 초기화한다.

3. 0부터 length까지 idx를 증가시키며 아래를 수행한다.
- num에 idx번째 문자를 0('A') ~ 25('Z')까지 변환하여 넣어준다.
- chars의 num번째 값을 증가시킨다.
- chars의 num번째 값이 max보다 큰 경우, max에 chars의 num번째 값을 넣어준다.
- 연속된 문자열의 길이인 $idx - start + 1$의 값이 $max + k$보다 큰 경우, charArray의 start번째 문자를 0('A') ~ 25('Z')까지 변환한 값을 이용하여 chars의 해당 위치의 값을 감소시키고 시작 위치인 start를 증가시킨다.
- maxLength에 maxLength와 $idx - start + 1$의 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 최대 길이를 저장한 maxLength를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestRepeatingCharacterReplacement.java){:target="_blank"}에서 확인 가능합니다.