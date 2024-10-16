---
title: "Leetcode Java Number of Matching Subsequences"
excerpt: "Leetcode Number of Matching Subsequences Java"
last_modified_at: 2023-01-03T19:50:00
header:
  image: /assets/images/leetcode/number-of-matching-subsequences.png
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
[Link](https://leetcode.com/problems/number-of-matching-subsequences){:target="_blank"}

# 코드
```java
class Solution {

  public int numMatchingSubseq(String s, String[] words) {
    Map<String, Integer> map = new HashMap<>();
    for (String word : words) {
      map.put(word, map.getOrDefault(word, 0) + 1);
    }
    int count = 0;
    char[] sCharArray = s.toCharArray();
    for (String word : map.keySet()) {
      char[] wordCharArray = word.toCharArray();
      int i = 0;
      int j = 0;
      while (i < sCharArray.length && j < wordCharArray.length) {
        if (sCharArray[i] == wordCharArray[j]) {
          j++;
        }
        i++;
      }
      if (j == wordCharArray.length) {
        count += map.get(word);
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-matching-subsequences/submissions/870372348/){:target="_blank"}

# 설명
1. words 배열 내 s의 부분 수열의 개수를 구하는 문제이다.
- "abc"와 "ace"는 "abcde"의 부분 수열이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 words 내 중복된 문자열의 개수를 저장할 변수로, words를 이용하여 문자별 발생 횟수를 값에 넣어준다.
- count는 words 배열 내 s의 부분 수열의 개수를 저장할 변수로, 0으로 초기화한다.
- sCharArray는 s를 문자 배열로 저장한 변수이다.

3. map의 키 값들을 차례대로 word로 넣어 아래를 반복한다.
- 부분 수열 검증에 필요한 변수들을 정의한다.
  - wordCharArray는 word를 문자 배열로 저장한 변수이다.
  - i와 j는 s와 word의 각 문자 배열을 차례대로 검증할 변수로, 모두 0으로 초기화한다.
- i가 sCharArray의 길이 미만이고 j가 wordCharArray의 길이 미만일 때 까지 아래를 반복하여 수행한다.
  - sCharArray의 i번째 문자와 wordCharARray의 j번째 문자가 동일한 경우, j를 다음 위치로 이동시킨다.
  - i를 증가시켜 sCharArray의 다음 위치로 이동시켜준다.
- j가 wordCharArray의 길이와 동일한 경우, 부분 순열에 속하므로 count에 map의 word에 해당하는 개수를 더해준다.

4. 반복이 완료되면 words 배열 내 s의 부분 수열의 개수를 저장한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfMatchingSubsequences.java){:target="_blank"}에서 확인 가능합니다.