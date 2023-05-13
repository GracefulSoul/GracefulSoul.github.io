---
title: "Leetcode Java Count Ways To Build Good Strings"
excerpt: "Leetcode Count Ways To Build Good Strings Java"
last_modified_at: 2023-05-13T12:55:00
header:
  image: /assets/images/leetcode/count-ways-to-build-good-strings.png
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
[Link](https://leetcode.com/problems/count-ways-to-build-good-strings){:target="_blank"}

# 코드
```java
class Solution {

  public int countGoodStrings(int low, int high, int zero, int one) {
    int result = 0;
    int mod = 1000000007;
    int dp[] = new int[high + 1];
    dp[0] = 1;
    for (int i = 1; i <= high; i++) {
      if (i >= zero) {
        dp[i] = (dp[i] + dp[i - zero]) % mod;
      }
      if (i >= one) {
        dp[i] = (dp[i] + dp[i - one]) % mod;
      }
      if (i >= low) {
        result = (result + dp[i]) % mod;
      }
    }
    return result;
  }
}
```

# 결과
[Link](https://leetcode.com/problems/count-ways-to-build-good-strings/submissions/949323853/){:target="_blank"}

# 설명
1. zero, one, low, high를 이용하여 아래의 하나를 수행하여 만들어진 문자열들 중 양호한 문자열의 수를 계산하는 문제이다.
- 양호한 문자열이란 아래 수행을 이용하여 low와 high 사이의 길이를 갖는 문자열이다.
  - 문자 '0'을 zero번 이어준다.
  - 문자 '1'을 one번 이어준다.
  - 이 작업은 여러 번 수행 가능하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 넣을 변수로, 0으로 초기화한다.
- mod는 모듈러를 적용할 변수로, $10^9 +7$로 초기화한다.
- dp는 양호한 문자열의 수를 계산하기 위한 변수로, $high + 1$ 크기의 정수 배열로 초기화하고 첫 값을 1로 초기화한다.

3. 1부터 high 미만까지 i를 증가시키며 아래를 수행한다.
- i가 zero보다 큰 경우, dp[i]에 dp[i]의 값과 dp[$i - zero$]의 값인 $i - zero$번째 양호한 문자열의 수를 더한 값에 mod를 나눈 나머지 값을 넣어준다.
- i가 one보다 큰 경우, dp[i]에 dp[i]의 값과 dp[$i - one$]의 값인 $i - one$번째 양호한 문자열의 수를 더한 값에 mod를 나눈 나머지 값을 넣어준다.
- i가 low보다 큰 경우 양호한 문자열의 수 범위에 포함되므로, 결과를 저장할 result에 result와 dp[i]의 값을 더한 후 mod를 나눈 나머지 값을 넣어준다.

4. 반복이 완료되면 양호한 문자열의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountWaysToBuildGoodStrings.java){:target="_blank"}에서 확인 가능합니다.