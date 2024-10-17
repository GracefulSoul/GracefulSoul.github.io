---
title: "Leetcode Java Count the Number of Consistent Strings"
excerpt: "Leetcode Easy - 'Count the Number of Consistent Strings' 문제 Java 풀이"
last_modified_at: 2024-09-12T18:00:00
header:
  image: /assets/images/leetcode/count-the-number-of-consistent-strings.png
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
[Link](https://leetcode.com/problems/count-the-number-of-consistent-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public int countConsistentStrings(String allowed, String[] words) {
    int result = words.length;
    int[] count = new int[26];
    for (char c : allowed.toCharArray()) {
      count[c - 'a']++;
    }
    for (String word : words) {
      for (char c : word.toCharArray()) {
        if (count[c - 'a'] == 0) {
          result--;
          break;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-the-number-of-consistent-strings/submissions/1387488828/){:target="_blank"}

# 설명
1. allowed 문자열 내 존재하는 문자들로만 이루어진 words 내 문자열 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 조건을 만족하는 words 내 문자열의 갯수를 저장할 변수로, 우선 words의 모든 문자열의 갯수로 초기화한다.
- count는 allowed 내 문자 갯수를 저장할 변수로, 영문자 갯수인 26 크기의 정수 배열로 초기화하여 allowed 내 문자 갯수를 넣어준다.

3. words의 각 문자열을 순차적으로 word에 넣어 아래를 수행한다.
- word의 각 문자들을 순차적으로 c에 넣어 아래를 수행한다.
  - count 내 해당 문자열 순서 위치 값이 0인 allowed 내 존재하지 않는 문자인 경우, 허용되지 않는 문자가 포함된 문자열이므로 result를 감소시키고 반복을 중지한다.

4. 반복이 완료되면 words 내 allowed 내 문자로 이루어진 문자열 의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountTheNumberOfConsistentStrings.java){:target="_blank"}에서 확인 가능합니다.