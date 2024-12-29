---
title: "Leetcode Java Number of Ways to Form a Target String Given a Dictionary"
excerpt: "Leetcode - 'Number of Ways to Form a Target String Given a Dictionary' 문제 Java 풀이"
last_modified_at: 2024-12-29T15:20:00
header:
  image: /assets/images/leetcode/number-of-ways-to-form-a-target-string-given-a-dictionary.png
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
[Link](https://leetcode.com/problems/number-of-ways-to-form-a-target-string-given-a-dictionary/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int MOD = 1000000007;

  public int numWays(String[] words, String target) {
    int length = target.length();
    long[] dp = new long[length + 1];
    dp[0] = 1;
    for (int i = 0; i < words[0].length(); i++) {
      int[] count = new int[26];
      for (String word : words) {
        count[word.charAt(i) - 'a']++;
      }
      for (int j = length - 1; j >= 0; j--) {
        dp[j + 1] += (dp[j] * count[target.charAt(j) - 'a']) % MOD;
      }
    }
    return (int) (dp[length] % MOD);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-ways-to-form-a-target-string-given-a-dictionary/submissions/1491301276/){:target="_blank"}

# 설명
1. words를 이용하여 target 문자열을 구성할 수 있는 방법의 수를 계산하는 문제이다.
- 단, 방법의 수가 매우 클 수 있으므로, 모듈러 $10^9 + 7$을 적용한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 target 문자열의 길이를 저장한 변수이다.
- dp는 방법의 수를 계산하기 위한 변수로, $length + 1$ 크기의 long 배열로 초기화하여 첫 값에 1을 넣어준다.

3. 0부터 words[0]의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- count는 각 문자 갯수를 계산할 변수로, words 내 문자열들의 문자 갯수를 계산하여 넣어준다.
- $length - 1$부터  0 이상까지 j를 감소시키며, dp[$j + 1$]에 아래 두 값을 곱한 값을 MOD로 나눈 나머지 값을 더해준다.
  - dp[j]인 이전 위치까지 구성하기위한 방법의 수.
  - target의 j번째 문자에 해당하는 count 값인 현재 문자를 넣을 방법의 수.

4. 반복이 완료되어 계산된 방법을 다시 MOD로 나눈 나머지 값을 int형으로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfWaysToFormATargetStringGivenADictionary.java){:target="_blank"}에서 확인 가능합니다.