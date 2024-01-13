---
title: "Leetcode Java Minimum Number of Steps to Make Two Strings Anagram"
excerpt: "Leetcode Minimum Number of Steps to Make Two Strings Anagram Java"
last_modified_at: 2024-01-13T13:20:00
header:
  image: /assets/images/leetcode/minimum-number-of-steps-to-make-two-strings-anagram.png
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
[Link](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram){:target="_blank"}

# 코드
```java
class Solution {

  public int minSteps(String s, String t) {
    int[] count = new int[26];
    for (int i = 0; i < s.length(); i++) {
      count[s.charAt(i) - 'a']++;
      count[t.charAt(i) - 'a']--;
    }
    int result = 0;
    for (int num : count) {
      if (num > 0) {
        result += num;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/submissions/1144726357/){:target="_blank"}

# 설명
1. 문자열 t의 일부 문자들을 변경하여 s를 구성할 수 있는 [Anagram](https://en.wikipedia.org/wiki/Anagram){:target="_blank"} 문자열로 변환하기위한 최소 횟수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 s와 t의 문자 갯수를 가감할 변수로, 영문자의 갯수인 26 크기의 정수 배열로 초기화하여 s와 t를 반복하여 문자 갯수를 계산하여 넣어준다.
- result는 결과를 저장할 변수로, 0으로 초기화하고 count를 반복하여 0 초과인 값을 넣어준다.

3. 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfStepsToMakeTwoStringsAnagram.java){:target="_blank"}에서 확인 가능합니다.