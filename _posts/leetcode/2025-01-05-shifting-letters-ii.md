---
title: "Leetcode Java Shifting Letters II"
excerpt: "Leetcode - 'Shifting Letters II' 문제 Java 풀이"
last_modified_at: 2025-01-05T20:10:00
header:
  image: /assets/images/leetcode/shifting-letters-ii.png
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
[Link](https://leetcode.com/problems/shifting-letters-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public String shiftingLetters(String s, int[][] shifts) {
    int length = s.length();
    int[] dp = new int[length + 1];
    for (int[] shift : shifts) {
      int end = shift[1] + 1;
      int weight = shift[2] == 1 ? 1 : -1;
      dp[shift[0]] += weight;
      if (end < length) {
        dp[end] -= weight;
      }
    }
    int curr = 0;
    for (int i = 0; i < length; i++) {
      curr += dp[i];
      dp[i] = curr;
    }
    StringBuilder sb = new StringBuilder(s);
    for (int i = 0; i < length; i++) {
      sb.setCharAt(i, (char) ('a' + (s.charAt(i) - 'a' + (((dp[i] % 26) + 26) % 26)) % 26));
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shifting-letters-ii/submissions/1498420768/){:target="_blank"}

# 설명
1. s의 각 문자들을 아래의 조건을 만족하는 shifts를 수행한 결과를 반환하는 문제이다.
- shifts[i] = [start<sub>i</sub>, end<sub>i</sub>, direction<sub>i</sub>]를 만족하며, start<sub>i</sub>번째 문자부터 end<sub>i</sub>번째 문자까지 direction<sub>i</sub>의 값에 따라 영문자를 변환하는 문제이다.
- direction<sub>i</sub>가 1인 경우, [start, end] 범위의 각 문자들을 다음 문자들로 바꿔주고 'z'는 'a'로 변경한다.
- direction<sub>i</sub>가 0인 경우, [start, end] 범위의 각 문자들을 이전 문자들로 바꿔주고 'a'는 'z'로 변경한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 s의 길이를 저장한 변수이다.
- dp는 각 문자 위치 별 가감해야 하는 값들을 산정하기 위한 변수로, shifts의 값을 순차적으로 반복하여 dp의 [start, end] 범위 값들에 direction에 따라 1이면 1을 더하고 0은 1을 빼준다.
  - 먼저 start와 end에 가중치만 넣은 이후, 다시 반복을 수행하면서 가중치를 가감하면서 dp에 넣어준다.
- sb는 결과 문자열을 넣기 위한 변수로, s를 넣어 초기화한다.

3. 0부터 length까지 i를 증가시키며, 각 i번째 위치 문자를 dp[i]번 값에 따라 차감하여 변환된 문자로 변환하여 넣어준다.

4. 반복이 완료되어 변환된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShiftingLettersII.java){:target="_blank"}에서 확인 가능합니다.