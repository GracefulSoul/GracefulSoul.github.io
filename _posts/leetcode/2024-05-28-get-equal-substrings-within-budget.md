---
title: "Leetcode Java Get Equal Substrings Within Budget"
excerpt: "Leetcode Get Equal Substrings Within Budget Java"
last_modified_at: 2024-05-28T20:40:00
header:
  image: /assets/images/leetcode/get-equal-substrings-within-budget.png
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
[Link](https://leetcode.com/problems/get-equal-substrings-within-budget/){:target="_blank"}

# 코드
```java
class Solution {

  public int equalSubstring(String s, String t, int maxCost) {
    char[] sCharArray = s.toCharArray();
    char[] tCharArray = t.toCharArray();
    int i = 0;
    int j = 0;
    while (j < s.length()) {
      maxCost -= Math.abs(sCharArray[j] - tCharArray[j++]);
      if (maxCost < 0) {
        maxCost += Math.abs(sCharArray[i] - tCharArray[i++]);
      }
    }
    return j - i;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/get-equal-substrings-within-budget/submissions/1271253962/){:target="_blank"}

# 설명
1. 동일한 길이의 문자열 s와 t를 이용하여 maxCost 이하의 비용으로 t의 부분 문자열의 문자를 변경하여 s의 부분 문자열이 동일하게 만들 경우, 가능한 최대 길이의 부분 문자열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sCharArray와 tCharArray는 s와 t를 문자 배열로 변환한 변수이다.
- i와 j는 문자열의 시작 위치와 종료 위치를 저장할 변수로, 둘 다 0으로 초기화한다.

3. j가 s의 길이 미만일 때 까지 아래를 반복한다.
- maxCoust에 $sCharArray[j] - tCharArray[j]$의 절댓값을 빼주고 j를 증가시킨다.
- maxCoust가 0보다 낮은 경우 시작 위치를 증가시키기 위해서, maxCoust에 $sCharArray[i] - tCharArray[i]$의 절댓값을 더해주고 i를 증가시킨다.

4. 반복이 완료되면 문자열의 길이인 $j - i$를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GetEqualSubstringsWithinBudget.java){:target="_blank"}에서 확인 가능합니다.