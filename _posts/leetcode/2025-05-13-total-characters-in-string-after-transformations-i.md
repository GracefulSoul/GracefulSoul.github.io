---
title: "Leetcode Java Total Characters in String After Transformations I"
excerpt: "Leetcode - 'Total Characters in String After Transformations I' 문제 Java 풀이"
last_modified_at: 2025-05-13T19:00:00
header:
  image: /assets/images/leetcode/total-characters-in-string-after-transformations-i.png
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
[Link](https://leetcode.com/problems/total-characters-in-string-after-transformations-i/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int MOD = 1000000007;

  public int lengthAfterTransformations(String s, int t) {
    int[] dp = new int[t + 26];
    for (int i = 0; i < 26; i++) {
      dp[i] = 1;
    }
    for (int i = 26; i < t + 26; i++) {
      dp[i] = (dp[i - 25] + dp[i - 26]) % MOD;
    }
    int result = 0;
    for (char c : s.toCharArray()) {
      result = (result + dp[c - 'a' + t]) % MOD;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/total-characters-in-string-after-transformations-i/submissions/1632696192/){:target="_blank"}

# 설명
1. 영소문자로 이루어진 s를 이용하여 아래 규칙을 t번 수행한 결과에 대한 문자열 길이를 반환하는 문제이다.
- 'a'는 'b'로 'b'는 'c'와 같이 각 영소문자는 각 수행에서 다음 영소문자로 변환하고, 'z' 문자는 'ab' 문자열로 변환한다.
- 길이가 매우 길 수 있으므로 모듈러 $10^9 + 7$을 적용한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 각 수행 별 영소문자의 갯수를 계산할 변수로, 영소문자 갯수인 26과 반복 횟수인 t를 더한 크기로 초기화 후 아래를 수행하여 값을 넣어준다.
  - dp 내 모든 위치 값에 1을 넣어 초기값을 넣어준다.
  - 26부터 $t + 26$ 미만까지 i를 증가시키며 dp[i]의 값에 $dp[i - 25] + dp[i - 26]$의 값인 현재 반복을 수행한 결과에 모듈러 $10^9 + 7$을 적용한 값을 넣어준다.
- result는 문자열의 길이를 저장할 변수로, 0으로 초기화한다.

3. s의 각 문자를 순서대로 c에 넣어 아래를 수행한다.
- result에 result와 dp 내 c의 영문자 순서에 t를 더한 위치 값을 더한 후 모듈러 $10^9 + 7$을 적용한 값을 넣어준다.

4. 반복이 완료되어 계산된 문자열의 길이인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TotalCharactersInStringAfterTransformationsI.java){:target="_blank"}에서 확인 가능합니다.