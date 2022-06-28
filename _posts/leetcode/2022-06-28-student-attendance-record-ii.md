---
title: "Leetcode Java Student Attendance Record II"
excerpt: "Leetcode Student Attendance Record II Java"
last_modified_at: 2022-06-28T20:00:00
header:
  image: /assets/images/leetcode/student-attendance-record-ii.png
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
[Link](https://leetcode.com/problems/student-attendance-record-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int checkRecord(int n) {
    int[] dp = new int[] { 1, 1, 0, 1, 0, 0 };
    for (int idx = 2; idx <= n; idx++) {
      dp = new int[] { this.getSum(dp, 0, 2), dp[0], dp[1], this.getSum(dp, 0, 5), dp[3], dp[4] };
    }
    return this.getSum(dp, 0, 5);
  }

  private int getSum(int[] dp, int low, int high) {
    int sum = 0;
    for (int idx = low; idx <= high; idx++) {
      sum = (sum + dp[idx]) % 1000000007;
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/733342960/){:target="_blank"}

# 설명
1. 아래의 각 문자 별 출석 상태를 기준으로 개근상을 받을 수 있는 n개의 가능한 출석 기록 수를 반환하는 문제이다.
- 'A'는 결석을 의미한다.
- 'L'은 지각을 의미한다.
- 'P'는 출석을 의미한다.
- 위 세 값을 이용하여 1번 이하의 결석과 3번 연속 지각하지 않으면 개근상을 받을 수 있다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. dp에 n이 1일 경우 받을 수 있는 경우인 [1, 1, 0, 1, 0, 0]으로 초기화한다.
- n이 1일 경우, 아래와 같다.
  - | A0L0 | P | 
| A0L1 | L |
| A0L2 |  |
| A1L0 | A |
| A1L1 |  |
| A1L2 |  |
- n이 2일 경우, 아래와 같다.
  - | A0L0 | LP, PP | 
| A0L1 | PL |
| A0L2 | LL |
| A1L0 | AP, LA, PA |
| A1L1 | AL |
| A1L2 |  |

3. 2번의 계산 식을 이용하여 2부터 n까지 idx를 증가시키며 아래의 계산을 반복한다.
- $dp[0] = dp[0] + dp[1] + dp[2]$
- $dp[1] = dp[0]$
- $dp[2] = dp[1]$
- $dp[3] = dp[0] + ... + dp[5]$
- $dp[4] = dp[3]$
- $dp[5] = dp[4]$
- 단, 모듈러 $10^9 +7$을 이용해야 하므로 모든 계산에 getSum(int[] dp, int low, int high) 메서드를 이용하여 $10^9 +7$을 나누어 수행해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StudentAttendanceRecordII.java){:target="_blank"}에서 확인 가능합니다.