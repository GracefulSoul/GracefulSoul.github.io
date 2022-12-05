---
title: "Leetcode Java Shortest Completing Word"
excerpt: "Leetcode Shortest Completing Word Java"
last_modified_at: 2022-12-05T10:50:00
header:
  image: /assets/images/leetcode/shortest-completing-word.png
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
[Link](https://leetcode.com/problems/shortest-completing-word){:target="_blank"}

# 코드
```java
class Solution {

  public String shortestCompletingWord(String licensePlate, String[] words) {
    int[] licenseChars = this.getCharCounts(licensePlate);
    String result = null;
    for (String word : words) {
      if ((result == null || result.length() > word.length()) && this.isCompletingWord(licenseChars, this.getCharCounts(word))) {
        result = word;
      }
    }
    return result;
  }

  private boolean isCompletingWord(int[] licenseChars, int[] wordChars) {
    for (int idx = 0; idx < 26; idx++) {
      if (licenseChars[idx] != 0 && licenseChars[idx] > wordChars[idx]) {
        return false;
      }
    }
    return true;
  }

  private int[] getCharCounts(String s) {
    int[] charCounts = new int[26];
    for (char c : s.toCharArray()) {
      if (Character.isLetter(c)) {
        charCounts[Character.toLowerCase(c) - 'a']++;
      }
    }
    return charCounts;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/854769720/){:target="_blank"}

# 설명
1. wordChars에서 licensePlate에 존재하는 영문자가 모두 포함된 최소 길이의 문자열을 찾아 반환하는 문제이다.
- 정답이 여러 개인 경우, 첫 번째로 일치하는 문자열을 반환한다.

2. 문자열에 포함된 영문자의 갯수를 반환하는 getCharCounts(String s) 메서드를 먼저 정의한다.
- charCounts는 영문자의 갯수를 저장하기 위한 배열로, 영문자의 수인 26 크기로 초기화한다.
- s의 모든 단어를 반복하여 영문자에 해당하는 경우, 소문자로 변경하여 charCounts에 'a'는 0부터 'z'는 25까지 위치에 넣어준다.
- 모든 영문자 갯수를 저장한 charCounts를 반환한다.

3. licensePlate에 존재하는 문자들이 wordChars 내 특정 문자열에 모두 포함되었는지 검증하기 위한 isCompletingWord(int[] licenseChars, int[] wordChars) 메서드를 완성한다.
- 영문자의 크기인 0부터 26 미만까지 idx를 증가시키며 아래를 검증한다.
  - licenseChars의 idx번째 값이 0이 아니면서 licenseChars의 idx번째 문자의 갯수가 wordChars의 idx번째 문자 갯수보다 큰 경우, licensePlate의 모든 영문자가 word에 포함되어 있지 않으므로 false를 반환한다.
- 반복이 완료되면 모두 포함된 경우이므로, true를 반환한다.

4. 문제 풀이에 필요한 변수를 정의한다.
- licenseChars는 licensePlate 내 포함된 영문자의 갯수를 저장할 변수로, 2번에서 정의한 getCharCounts(String s) 메서드를 수행한 결과를 넣어준다.
- result는 주어진 조건을 만족하는 최소 길이의 문자열을 저장할 변수로, null로 초기화한다.

5. words의 모든 단어를 word에 넣어 아래를 반복 수행한다.
- 아래의 조건을 모두 만족하는 경우, word가 기존보다 더 짧은 첫 문자열이므로 result에 word를 넣어준다.
  - reulst가 null인 첫 단어이거나 result의 길이가 word보다 더 긴 단어인 경우.
  - licenseChars와 word를 이용하여 2번에서 정의한 getCharCounts(String s) 메서드를 수행한 결과를 3번에서 정의한 isCompletingWord(int[] licenseChars, int[] wordChars) 메서드를 수행한 결과가 true인 모두 포함된 단어로 검증된 경우.

6. 반복이 완료되면 조건을 만족하는 문자열인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestCompletingWord.java){:target="_blank"}에서 확인 가능합니다.