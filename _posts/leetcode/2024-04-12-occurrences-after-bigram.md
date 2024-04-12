---
title: "Leetcode Java Occurrences After Bigram"
excerpt: "Leetcode Occurrences After Bigram Java"
last_modified_at: 2024-04-12T18:10:00
header:
  image: /assets/images/leetcode/occurrences-after-bigram.png
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
[Link](https://leetcode.com/problems/occurrences-after-bigram/){:target="_blank"}

# 코드
```java
class Solution {

  public String[] findOcurrences(String text, String first, String second) {
    String[] words = text.split(" ");
    List<String> result = new ArrayList<>();
    for (int i = 2; i < words.length; i++) {
      if (first.equals(words[i - 2]) && second.equals(words[i - 1])) {
        result.add(words[i]);
      }
    }
    return result.toArray(new String[] {});
  }

}
```

# 결과
[Link](https://leetcode.com/problems/occurrences-after-bigram/submissions/1230215801/){:target="_blank"}

# 설명
1. 띄어쓰기로 각 문자열이 구분된 text 문자열에서 first 문자열 다음 second 문자열이 나온 다음 문자열인 third 문자열들을 모아 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- words는 test를 띄어쓰기 단위로 분리하여 저장한 문자열 배열이다.
- result는 third 문자열을 모으기 위한 변수로, ArrayList로 초기화한다.

3. 2부터 words의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- first와 words[$i - 2$] 문자열이 같으면서 second와 words[$i - 1$] 문자열이 같은 경우, result에 words[i]를 넣어준다.

4. 반복이 완료되면 조건에 만족하는 third 문자열만 모은 result를 문자열 배열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OccurrencesAfterBigram.java){:target="_blank"}에서 확인 가능합니다.