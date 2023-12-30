---
title: "Leetcode Java Redistribute Characters to Make All Strings Equal"
excerpt: "Leetcode Redistribute Characters to Make All Strings Equal Java"
last_modified_at: 2023-12-30T09:55:00
header:
  image: /assets/images/leetcode/redistribute-characters-to-make-all-strings-equal.png
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
[Link](https://leetcode.com/problems/redistribute-characters-to-make-all-strings-equal){:target="_blank"}

# 코드
```java
class Solution {

  public boolean makeEqual(String[] words) {
    int length = words.length;
    if (length == 1) {
      return true;
    }
    int wordsLength = 0;
    for (String word : words) {
      wordsLength += word.length();
    }
    if (wordsLength % length != 0) {
      return false;
    }
    int[] counts = new int[26];
    for (String word : words) {
      for (char c : word.toCharArray()) {
        counts[c - 'a']++;
      }
    }
    for (int count : counts) {
      if (count % length != 0) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/redistribute-characters-to-make-all-strings-equal/submissions/1131803110/){:target="_blank"}

# 설명
1. words의 모든 문자열의 특정 단어를 다른 문장으로 이동하여 모든 문자열이 동일하게 구성할 수 있는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 words의 길이를 저장한 변수이다.
  - length가 1로, 문자열이 1개만 존재하면 true를 주어진 문제의 결과로 반환한다.
- wordsLength는 words의 모든 문자열의 길이를 저장한 변수로, words를 반복하여 모든 문자열의 길이를 저장한다.
  - wordsLength를 length로 나눌 수 없으면, 동일한 문자열 구성이 불가능하므로 false를 주어진 문제의 결과로 반환한다.
- counts는 문자들의 갯수를 저장할 변수로, 영문자 갯수인 26 크기의 정수 배열로 초기화한 후 words를 반복하여 모든 문자의 갯수를 계산해준다.

3. counts를 반복하여 각 문자의 갯수가 length 배수가 아니라면 주어진 문제의 결과로 false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 동일한 문자열로 동일하게 구성할 수 있으므로, true를 주어진 문제의 결과로 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RedistributeCharactersToMakeAllStringsEqual.java){:target="_blank"}에서 확인 가능합니다.