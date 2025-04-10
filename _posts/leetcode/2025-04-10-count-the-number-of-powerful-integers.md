---
title: "Leetcode Java Count the Number of Powerful Integers"
excerpt: "Leetcode - 'Count the Number of Powerful Integers' 문제 Java 풀이"
last_modified_at: 2025-04-10T19:15:00
header:
  image: /assets/images/leetcode/count-the-number-of-powerful-integers.png
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
[Link](https://leetcode.com/problems/count-the-number-of-powerful-integers/){:target="_blank"}

# 코드
```java
class Solution {

  public long numberOfPowerfulInt(long start, long finish, int limit, String s) {
    return this.numberOfPowerfulInt(finish, limit, s) - this.numberOfPowerfulInt(start - 1, limit, s);
  }

  private long numberOfPowerfulInt(long num, int limit, String s) {
    String str = Long.toString(num);
    int length = str.length() - s.length();
    if (length < 0) {
      return 0;
    } else {
      long[][] dp = new long[length + 1][2];
      dp[length][0] = 1;
      dp[length][1] = str.substring(length).compareTo(s) >= 0 ? 1 : 0;
      for (int i = length - 1; i >= 0; i--) {
        int curr = str.charAt(i) - '0';
        dp[i][0] = (limit + 1) * dp[i + 1][0];
        if (curr <= limit) {
          dp[i][1] = (curr * dp[i + 1][0]) + dp[i + 1][1];
        } else {
          dp[i][1] = dp[i][0];
        }
      }
      return dp[0][1];
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-the-number-of-powerful-integers/submissions/1602617642/){:target="_blank"}

# 설명
1. 각 자리가 limit보다 낮은 [start, finish] 범위 내 값들 중 s로 끝나는 숫자들의 갯수를 계산하는 문제이다.

2. 특정 값 내 조건을 만족하는 숫자의 갯수를 계산하기 위한 numberOfPowerfulInt(long num, int limit, String s) 메서드를 정의한다.
- 메서드 수행에 필요한 변수를 정의한다.
  - str은 num을 문자열로 변환한 변수이다.
  - length는 str과 s의 길이 차이를 저장한 변수이다.
- length가 0보다 작아 s로 끝날 수 없는 경우, 0을 반환한다.
- length가 0보다 큰 경우, 아래를 계속 수행한다.
- dp는 갯수를 계산하기 위한 변수로, $(length + 1) \times 2$ 크기의 2차원 long 배열로 초기화 후 마지막 위치에 아래 값을 넣어준다.
  - dp[length][0] 값에는 1을 넣어준다.
  - dp[length][1] 값에는 str의 length만큼 자른 숫자가 s보다 큰 경우 1을, 아니면 0을 넣어준다.
- $length -1$부터 0 이상까지 i를 감소시키며 아래를 반복한다.
  - curr에 str의 i번째 문자를 숫자로 변환하여 넣어준다.
  - dp[i][0]에 $(limit + 1) \times dp[i + 1][0]$인 이전까지 값들의 갯수를 앞자리 limit 이하의 갯수만큼 곱한 값을 넣어준다.
  - curr이 limit보다 작은 경우, dp[i][1]의 위치에 $(curr \times dp[i + 1][0]) + dp[i + 1][1]$인 앞자리 이전까지 값의 갯수를 curr 이하의 갯수만큼 곱한 값에 이전까지 계산된 값을 더한 값을 넣어준다.
  - curr이 limit보다 큰 경우, dp[i][1]의 위치에 기본 갯수인 dp[i][0]의 값을 넣어준다.
- 반복이 완료되면 계산된 갯수인 dp[0][1]의 값을 반환한다.

3. 2번에서 정의한 numberOfPowerfulInt(long num, int limit, String s) 메서드를 num에 finish를 넣어 수행한 값에 start를 넣어 수행한 값을 뺀 [start, finish] 범위 내 조건에 만족하는 갯수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountTheNumberOfPowerfulIntegers.java){:target="_blank"}에서 확인 가능합니다.