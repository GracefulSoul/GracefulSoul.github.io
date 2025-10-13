---
title: "Leetcode Java Find Resultant Array After Removing Anagrams"
excerpt: "Leetcode - 'Find Resultant Array After Removing Anagrams' 문제 Java 풀이"
last_modified_at: 2025-10-13T19:50:00
header:
  image: /assets/images/leetcode/find-resultant-array-after-removing-anagrams.png
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
[Link](https://leetcode.com/problems/find-resultant-array-after-removing-anagrams/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> removeAnagrams(String[] words) {
    String prev = "";
    List<String> result = new ArrayList<>();
    for (String word : words) {
      char[] charArray = word.toCharArray();
      Arrays.sort(charArray);
      String curr = String.valueOf(charArray);
      if (!curr.equals(prev)) {
        result.add(word);
        prev = curr;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-resultant-array-after-removing-anagrams/submissions/1800205110/){:target="_blank"}

# 설명
1. 주어진 문자열 배열인 words에서 아래 조건을 만족하지 않을 때 까지 반복 후 남은 문자열을 반환하는 문제이다.
- 인접한 두 문자열이 아나그램을 만족하는 경우, 뒷 문자열을 삭제한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- prev는 이전에 발생한 문자열을 저장할 변수이다.
- result는 결과를 저장할 변수로, ArrayList로 초기화한다.

3. words의 각 문자를 word에 넣어 아래를 수행한다.
- word를 오름차순으로 문자들을 정렬하고 prev와 동일하지 않은 아나그램을 만족하지 않는 경우, result에 word를 넣고 prev에 curr을 저장한다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindResultantArrayAfterRemovingAnagrams.java){:target="_blank"}에서 확인 가능합니다.