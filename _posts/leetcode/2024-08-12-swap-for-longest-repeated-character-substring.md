---
title: "Leetcode Java Swap For Longest Repeated Character Substring"
excerpt: "Leetcode Swap For Longest Repeated Character Substring Java"
last_modified_at: 2024-08-12T18:00:00
header:
  image: /assets/images/leetcode/swap-for-longest-repeated-character-substring.png
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
[Link](https://leetcode.com/problems/swap-for-longest-repeated-character-substring/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxRepOpt1(String s) {
    int[] counts = new int[26];
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    for (int i = 0; i < length; i++) {
      counts[charArray[i] - 'a']++;
    }
    int result = 0;
    for (int i = 0; i < length; i++) {
      char curr = charArray[i];
      int j = i;
      int count = 0;
      int diff = 0;
      while (j < length && (curr == charArray[j] || diff == 0) && count < counts[curr - 'a']) {
        if (curr != charArray[j]) {
          diff++;
        }
        count++;
        j++;
      }
      if (count < counts[charArray[i] - 'a'] && diff == 0) {
        count++;
      }
      result = Math.max(result, count);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/swap-for-longest-repeated-character-substring/submissions/1352937240/){:target="_blank"}

# 설명
1. 문자열 s에서 최대 두 문자의 위치를 바꿔 동일한 문자로 이루어진 가장 긴 부분 문자열의 길이를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 문자의 갯수를 저장할 변수로, 영문자 갯수인 26 크기의 정수 배열로 초기화하고 아래 두 변수를 활용하여 s의 각 문자 갯수를 넣어준다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.
- result는 동일한 문자로 이루어진 가장 긴 부분 문자열의 길이를 저장할 변수로, 0으로 초기화한다.

3.  0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- 반복에 필요한 변수를 정의한다.
  - curr은 charArray에서 현재 위치인 i번째 문자를 넣은 변수이다.
  - j는 이후 문자열 탐색을 위한 변수로, i로 초기화한다.
  - count는 동일한 문자로 이루어진 문자열의 갯수를 저장할 변수로, 0으로 초기화한다.
  - diff는 다른 문자의 갯수를 저장할 변수로, 0으로 초기화한다.
- j가 length 미만이면서 curr이 charArray[j]와 동일한 문자이거나 diff가 0이면서 count가 counts의 curr 문자 순서에 해당하는 값보다 작은 경우, 아래를 수행한다.
  - curr이 charArray[j]와 다른 문자인 경우, diff를 증가시켜준다.
  - 동일한 문자의 수인 count와 탐색 위치인 j를 증가시켜준다.
- count가 counts의 $charArray[i] - 'a'$번째 값보다 작고 diff가 0인 경우, 연결된 값을 변경하는 경우인 count를 증가시켜준다.
- result에 이전까지 최대 길이인 result와 현재 길이인 count 중 큰 값을 넣어준다.

4. 반복이 완료되면 동일한 문자로 이루어진 가장 긴 부분 문자열의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SwapForLongestRepeatedCharacterSubstring.java){:target="_blank"}에서 확인 가능합니다.