---
title: "Leetcode Java Find All Anagrams in a String"
excerpt: "Leetcode - 'Find All Anagrams in a String' 문제 Java 풀이"
last_modified_at: 2022-03-30T13:00:00
header:
  image: /assets/images/leetcode/find-all-anagrams-in-a-string.png
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
[Link](https://leetcode.com/problems/find-all-anagrams-in-a-string/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> findAnagrams(String s, String p) {
    List<Integer> result = new ArrayList<>();
    if (p.length() > s.length()) {
      return result;
    }
    int[] countP = new int[26];
    for (int idx = 0; idx < p.length(); idx++) {
      countP[p.charAt(idx) - 97]++;
    }
    int[] countS = new int[26];
    int idx = 0;
    int i = 0;
    while (idx < p.length() && idx < s.length()) {
      countS[s.charAt(idx++) - 97]++;
    }
    while (idx <= s.length()) {
      int j = 0;
      while (j < 26 && countP[j] == countS[j]) {
        j++;
      }
      if (j == 26) {
        result.add(i);
      }
      countS[s.charAt(i) - 97]--;
      i++;
      if (idx != s.length()) {
        countS[s.charAt(idx) - 97]++;
      }
      idx++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/670078444/){:target="_blank"}

# 설명
1. 문자열 s와 p가 주어지면, p를 이용한 아나그램이 가능한 위치를 모두 반환하는 문제이다.
- 아나그램이란 문자의 재 배열로 특정 문자열을 만들 수 있는 단어 또는 어구이다.

2. 결과를 저장할 result를 ArrayList로 초기화 하고 p의 길이가 s의 길이보다 길 경우 아나그램으로 재 배열해서 만들 수 없으므로, 아무것도 들어있지 않은 result를 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- countP는 p에 들어간 문자의 발생 횟수를 저장할 배열로, 영문자의 개수인 26 크기로 정의하고 p를 반복하여 각 문자 별 a(97)을 뺀 위치 값을 증가시켜준다.
- countS는 s에 들어간 문자의 발생 횟수를 저장할 배열로, 영문자의 개수인 26 크기로 정의한다.
- idx는 s를 순회하기 위한 위치 변수로, 0으로 초기화한다.
- i는 아나그램이 성립하는 위치 변수로, 0으로 초기화한다.

4. idx가 p와 s의 길이 미만까지 반복하여 countS에 해당 문자의 위치 값을 넣고 idx를 증가시킨다.

5. idx가 s의 길이 이하일 때까지 아래를 반복한다.
- j를 0으로 초기화 시키고, j가 26 미만이고 countP와 countS의 값이 동일한지 검증하여 j를 증가시킨다.
- j가 26이면 문자열이 동일하다는 의미이므로, result에 i를 넣어준다.
- countS에 문자열 s의 i번째 문자에 해당하는 위치의 값을 감소시켜 검증에 해당 문자를 배제하고 i를 증가시킨다.
- idx가 s의 길이가 아닌 경우, countS에 문자열 s의 idx번째 문자에 해당하는 위치 값을 증가시켜 count를 추가한다.
- idx를 증가시키고 반복을 계속 수행한다.

6. 반복이 완료되면 아나그램이 성립하는 모든 위치 값을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindAllAnagramsInAString.java){:target="_blank"}에서 확인 가능합니다.