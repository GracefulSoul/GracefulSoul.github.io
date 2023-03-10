---
title: "Leetcode Java Permutation in String"
excerpt: "Leetcode Permutation in String Java"
last_modified_at: 2022-07-13T19:00:00
header:
  image: /assets/images/leetcode/permutation-in-string.png
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
[Link](https://leetcode.com/problems/permutation-in-string/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkInclusion(String s1, String s2) {
    char[] s1CharArray = s1.toCharArray();
    char[] s2CharArray = s2.toCharArray();
    int start = 0;
    int end = 0;
    int[] count = new int[26];
    for (char c : s1CharArray) {
      count[c - 'a']++;
    }
    while (end < s2CharArray.length) {
      char curr = s2CharArray[end++];
      count[curr - 'a']--;
      while (count[curr - 'a'] < 0 && start < end) {
        count[s2CharArray[start++] - 'a']++;
      }
      if (end - start == s1CharArray.length) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/745963928/){:target="_blank"}

# 설명
1. s1의 [순열](https://en.wikipedia.org/wiki/Permutation){:target="_blank"}이 s2에 포함되어 있는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- s1CharArray는 s1을, s2CharArray는 s2를 문자의 배열로 변환하여 넣어준 변수이다.
- start와 end는 s2 문자열 내 s1의 순열이 포함되었는지 검증하기 위한 인덱스로, 둘 다 0으로 초기화한다.
- count는 s1의 문자 개수를 저장할 배열로, 알파벳 크기인 26 크기로 초기화 하고 s1을 반복하여 각 자리의 값을 증가시킨다.

3. end가 s2의 길이 미만까지 아래를 반복한다.
- curr에 s2의 end번째 문자를 넣어주고, end를 증가시키고, count의 curr번째 문자 위치의 값을 감소시켜준다.
- count의 curr번쨰 문자 위치의 값이 0보다 작고, start가 end보다 작은 순열의 기준이 되는 경우 아래를 계속 수행한다.
  - count 내 s2CharArray[start] 문자 위치의 값과 start를 증가시킨다.
- end - start가 s1CharArray의 길이와 동일하면 순열이 되는 경우이므로, true를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 순열이 될 수 없으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PermutationInString.java){:target="_blank"}에서 확인 가능합니다.