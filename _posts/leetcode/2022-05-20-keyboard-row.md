---
title: "Leetcode Java Keyboard Row"
excerpt: "Leetcode Keyboard Row Java"
last_modified_at: 2022-05-20T12:00:00
header:
  image: /assets/images/leetcode/keyboard-row.png
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
[Link](https://leetcode.com/problems/keyboard-row/){:target="_blank"}

# 코드
```java
class Solution {

  private static final String[] KEYBOARD_ROWS = { "qwertyuiop", "asdfghjkl", "zxcvbnm" };

  public String[] findWords(String[] words) {
    int[] positions = new int[26];
    for (int idx = 0; idx < KEYBOARD_ROWS.length; idx++) {
      for (char c : KEYBOARD_ROWS[idx].toCharArray()) {
        positions[c - 'a'] = idx + 1;
      }  
    }
    List<String> result = new ArrayList<>();
    for (String word : words) {
      int row = 0;
      int idx = 0;
      for (; idx < word.length(); idx++) {
        char c = word.charAt(idx);
        int num = c - (c >= 'a' ? 'a' : 'A');
        if (row == 0) {
          row = positions[num];
        } else if (row != positions[num]) {
          break;
        }
      }
      if (idx == word.length()) {
        result.add(word);
      }
    }
    return result.toArray(new String[result.size()]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/703138600/){:target="_blank"}

# 설명
1. words 내 키보드의 한 줄로 구성이 가능한 문자열을 반환하는 문제이다.
- 키보드 영문의 경우 첫 번째 행은 "qwertyuiop", 두 번째 행은 "asdfghjkl", 세 번째 행은 "zxcvbnm"로 구성이 된다.

2. 기본 판단의 기준이 되는 KEYBOARD_ROWS 배열을 정의하여, "qwertyuiop", "asdfghjkl", "zxcvbnm" 세 값을 넣어 전역 변수로 정의한다.

3. positions를 문자열의 크기인 26으로 정의하여, 모든 영문자 자리에 키보드 행의 위치를 넣어준다.

4. 결과를 넣을 result를 ArrayList로 초기화한다.

5. words를 반복하여 아래를 수행한다.
- 키보드의 행을 저장할 row와, word의 커서 역할을 할 idx를 0으로 초기화한다.
- idx를 word의 길이 미만까지 증가시키며 아래를 반복한다.
  - word의 idx번째 문자를 c에 넣어준다.
  - num에 c의 대소문자를 무시한 알파벳 순서를 넣어준다.
  - row가 0인 경우 첫 문자열이기 때문에 positions의 num번째 값을 넣어준다.
  - 위가 아니면서 row가 positions의 num번째 값과 다른 경우 키보드의 한 행을 이용하여 문자를 구상할 수 없으므로 반복을 종료한다.
- 반복이 종료되고 idx가 word의 length와 동일하면 한 행으로 단어를 구성 가능하므로, result에 word를 넣어준다.

6. 반복이 완료되면 result를 문자열의 배열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KeyboardRow.java){:target="_blank"}에서 확인 가능합니다.