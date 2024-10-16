---
title: "Leetcode Java Goat Latin"
excerpt: "Leetcode Goat Latin Java"
last_modified_at: 2023-01-31T23:00:00
header:
  image: /assets/images/leetcode/goat-latin.png
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
[Link](https://leetcode.com/problems/goat-latin){:target="_blank"}

# 코드
```java
class Solution {

  public String toGoatLatin(String sentence) {
    List<Character> vowels = Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U');
    String[] words = sentence.split("\\s");
    StringBuilder sb = new StringBuilder();
    StringBuilder temp = new StringBuilder();
    for (int i = 0; i < words.length; i++) {
      String word = words[i];
      if (vowels.contains(word.charAt(0))) {
        temp.append(word);
      } else {
        temp.append(word.substring(1, word.length()));
        temp.append(word.charAt(0));
      }
      temp.append("ma");
      for (int j = 0; j <= i; j++) {
        temp.append('a');
      }
      sb.append(temp);
      if (i != words.length - 1) {
        sb.append(' ');
      }
      temp.delete(0, sb.length());
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/goat-latin/submissions/888774200/){:target="_blank"}

# 설명
1. sentence 내 단어가 모음('a', 'e', 'i', 'o' 또는 'u')으로 시작하면 단어 끝에 'ma'를 추가하는 "Goat Latin"으로 변환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- vowels는 모음을 대소문자로 저장한 변수이다.
- words는 sentence를 띄어쓰기 단위로 분리한 단어들이 저장된 배열이다.
- sb는 결과 문자열을 넣을 변수로, StringBuilder로 초기화한다.
- temp는 각 단어들을 "Goat Latin"으로 동적 구성하기 위한 변수로, StringBuilder로 초기화한다.

3. 0부터 words의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- word에 words의 i번째 단어를 넣어 저장한다.
- word의 첫 문자가 vowels에 포함되는 모음으로 시작한 경우, temp에 word를 넣어준다.
- 위의 경우가 아니라면 두 번째 문자부터 temp에 넣고 마지막에 첫 번째 문자를 넣어준다.
- temp에 "ma" 문자열을 이어주고, $i + 1$개의 'a'를 이어준다.
- sb에 temp를 이어주고, 마지막 문자가 아닌 경우 띄어쓰기 문자(' ')를 넣어준다.
- temp를 0부터 sb의 길이만큼의 값들을 삭제하고 반복을 계속 수행한다.

4. 반복을 통해 "Goat Latin"으로 저장된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GoatLatin.java){:target="_blank"}에서 확인 가능합니다.