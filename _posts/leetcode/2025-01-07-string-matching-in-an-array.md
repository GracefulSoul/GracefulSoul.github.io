---
title: "Leetcode Java String Matching in an Array"
excerpt: "Leetcode - 'String Matching in an Array' 문제 Java 풀이"
last_modified_at: 2025-01-07T18:30:00
header:
  image: /assets/images/leetcode/string-matching-in-an-array.png
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
[Link](https://leetcode.com/problems/string-matching-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> stringMatching(String[] words) {
    String str = String.join(" ", words);
    List<String> result = new ArrayList<>();
    for (String word : words) {
      if (str.indexOf(word) != str.lastIndexOf(word)) {
        result.add(word);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/string-matching-in-an-array/submissions/1500510393/){:target="_blank"}

# 설명
1. words 내 임의 문장이 다른 문장의 부분 문자열인 경우를 중복되지 않게 모아 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- str은 words를 띄어쓰기 단위로 붙여 만든 변수이다.
- result는 결과를 넣을 변수이다.

3. words의 각 문자열을 순차적으로 word에 넣어 아래를 수행한다.
- str에 word의 처음 시작 위치와 마지막 위치가 다른 부분 문자열이 존재하는 경우, result애 word를 넣어준다.

4. 반복이 완료되어 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StringMatchingInAnArray.java){:target="_blank"}에서 확인 가능합니다.