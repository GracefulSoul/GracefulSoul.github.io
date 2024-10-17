---
title: "Leetcode Java Find Words That Can Be Formed by Characters"
excerpt: "Leetcode Easy - 'Find Words That Can Be Formed by Characters' 문제 Java 풀이"
last_modified_at: 2023-12-02T15:00:00
header:
  image: /assets/images/leetcode/find-words-that-can-be-formed-by-characters.png
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
[Link](https://leetcode.com/problems/find-words-that-can-be-formed-by-characters){:target="_blank"}

# 코드
```java
class Solution {

  public int countCharacters(String[] words, String chars) {
    int[] count = new int[26];
    for (char c : chars.toCharArray()) {
      count[c - 'a']++;
    }
    int result = 0;
    for (String word : words) {
      if (this.canBeFormed(count, word)) {
        result += word.length();
      }
    }
    return result;
  }

  private boolean canBeFormed(int[] count, String word) {
    int[] temp = new int[26];
    for (char c : word.toCharArray()) {
      int num = c - 'a';
      temp[num]++;
      if (temp[num] > count[num]) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-words-that-can-be-formed-by-characters/submissions/1110636758/){:target="_blank"}

# 설명
1. words 내 단어들 중 chars의 문자들로 구성할 수 있는 단어의 총 길이을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 chars의 단어의 갯수를 너헝줄 변수로, 26 크기의 정수 배열로 초기화 후 chars의 각 문자를 이용하여 count에 문자의 갯수를 넣어준다.
- result는 총 길이를 구하기 위한 변수로, 0으로 초기화한다.

3. words를 순차적으로 word에 넣어 아래를 반복한다.
- 4번에서 정의한 canBeFormed(int[] count, String word) 메서드를 수행한 결과가 true이 ㄴ경우, result에 word의 길이를 넣어준다.

4. 단어를 구성할 수 있는지 검증하기위한 canBeFormed(int[] count, String word) 메서드를 정의한다.
- temp는 word의 영문자 갯수를 구하기 위한 변수로, 동일하게 26 크기의 정수 배열로 초기화한다.
- word의 각 단어를 순차적으로 c에 넣어 아래를 반복한다.
  - num에 c를 'a'로 뺀 영문자 위치를 저장하고, temp[num]의 값을 증가시킨다.
  - temp[num]의 값이 count[num]보다 커지게 되면, 만들 수 없으므로 false를 반환한다.
- 반복이 완료되면 true를 반환한다.

5. 반복이 완료되면 총 단어의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindWordsThatCanBeFormedByCharacters.java){:target="_blank"}에서 확인 가능합니다.