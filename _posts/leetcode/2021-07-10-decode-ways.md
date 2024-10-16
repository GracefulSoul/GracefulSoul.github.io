---
title: "Leetcode Java Decode Ways"
excerpt: "Leetcode Decode Ways Java 풀이"
last_modified_at: 2021-07-10T17:00:00
header:
  image: /assets/images/leetcode/decode-ways.png
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
[Link](https://leetcode.com/problems/decode-ways/){:target="_blank"}

# 코드
```java
class Solution {

  public int numDecodings(String s) {
    int[] dp = new int[s.length() + 1];
    dp[s.length()] = 1;
    dp[s.length() - 1] = s.charAt(s.length() - 1) != '0' ? 1 : 0;
    for (int idx = s.length() - 2; idx >= 0; idx--) {
      if (s.charAt(idx) != '0') {
        dp[idx] = dp[idx + 1] + (Integer.parseInt(s.substring(idx, idx + 2)) <= 26 ? dp[idx + 2] : 0);
      }
    }
    return dp[0];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/520154233/){:target="_blank"}

# 설명
1. 숫자로 이루어진 주어진 문자열 s를 이용하여 아래의 규칙으로 만들 수 있는 문자열 조합에 대한 경우의 수를 구하는 문제이다.
- 각 문자는 숫자랑 치환이 된다. ('A' = "1", 'B' = "2", ..., 'Z' = "26")
- 주어진 문자열 s가 "26"일 경우 "2" + "6" = 'B' + 'F', "26" = 'Z'로 두 조합으로 구성이 가능하다.

2. 변수 dp를 주어진 문자열 s의 길이 + 1만큼의 크기인 정수 배열로 정의한다.

3. 정수 배열 dp의 초기 값을 설정한다.
- dp[s.length()]에는 1을 넣어준다.
- dp[s.length() - 1]에는 주어진 문자열 s의 마지막 문자가 '0'이 아닐 경우 1을, '0'일 경우 0을 넣어준다.

4. 문자열을 역순으로 모두 반복하여 문자열 조합에 대한 경우의 수를 구한다.
- 문자가 '0'이 아닌 경우 dp[i]에 dp[i + 1]의 값과 두 자리의 문자열이 26 이하인지 확인하여 26 이하일 경우 dp[i + 2] 값을 합쳐 넣어준다.
- 문자가 '0'이 나올 경우, 해당 문자 숫자열 치환이 불가능하므로 무시한다.

5. 반복이 완료되면 주어진 문자열 s의 첫 문자까지 확인하여 경우의 수를 산정한 dp[0]를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DecodeWays.java){:target="_blank"}에서 확인 가능합니다.