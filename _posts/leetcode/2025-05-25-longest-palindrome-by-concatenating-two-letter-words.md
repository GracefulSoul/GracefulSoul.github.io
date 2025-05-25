---
title: "Leetcode Java Longest Palindrome by Concatenating Two Letter Words"
excerpt: "Leetcode - 'Longest Palindrome by Concatenating Two Letter Words' 문제 Java 풀이"
last_modified_at: 2025-05-25T09:55:00
header:
  image: /assets/images/leetcode/longest-palindrome-by-concatenating-two-letter-words.png
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
[Link](https://leetcode.com/problems/longest-palindrome-by-concatenating-two-letter-words/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestPalindrome(String[] words) {
    int[][] counts = new int[26][26];
    int result = 0;
    for (String word : words) {
      int c1 = word.charAt(0) - 'a';
      int c2 = word.charAt(1) - 'a';
      if (counts[c2][c1] == 0) {
        counts[c1][c2]++;
      } else {
        result += 4;
        counts[c2][c1]--;
      }
    }
    for (int i = 0; i < 26; i++) {
      if (counts[i][i] > 0) {
        result += 2;
        break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-palindrome-by-concatenating-two-letter-words/submissions/1643527331/){:target="_blank"}

# 설명
1. words 내 문자열을 이용해서 회문(앞 뒤가 동일한 문자열)을 만들 수 있는 최대 문자열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 각 문자의 조합 갯수를 계산하기 위한 변수로, $26 \times 26$ 크기의 정수 배열로 초기화한다.
- length는 words의 길이를 저장한 변수이다.

3. words의 각 문자열을 word에 순차적으로 넣고 아래를 반복한다.
- c1과 c2는 word의 첫 번째 문자와 두 번째 문자의 영문자 순번을 넣어준다.
- counts[c2][c1]의 값이 0인 현재 문자열을 반대로 반전시킨 결과가 없는 경우, counts[c1][c2]의 값을 증가시켜준다.
- counts[c2][c1]의 값이 0보다 큰 현재 문자열을 반대로 반전시킨 결과가 있는 경우, 아래를 수행한다.
  - result 현재 문자와 이전 문자를 합친 문자열 길이인 4를 더해준다.
  - counts[c2][c1]인 반전시킨 문자열의 갯수를 감소시켜준다.

4. 마지막으로 0부터 26 미만까지 i를 증가시키며 동일 문자로 구성된 문자가 존재하는지 확인하여 존재하는 경우, result에 2를 더해준다.

5. 반복이 완료되면 만들 수 있는 회문의 최대 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestPalindromebyConcatenatingTwoLetterWords.java){:target="_blank"}에서 확인 가능합니다.