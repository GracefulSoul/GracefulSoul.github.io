---
title: "Leetcode Java Maximum Number of Events That Can Be Attended II"
excerpt: "Leetcode - 'Maximum Number of Events That Can Be Attended II' 문제 Java 풀이"
last_modified_at: 2025-07-08T18:10:00
header:
  image: /assets/images/leetcode/maximum-number-of-events-that-can-be-attended-ii.png
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
[Link](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxValue(int[][] events, int k) {
    if (k == 1) {
      return Arrays.stream(events).max(Comparator.comparingInt(e -> e[2])).orElseThrow()[2];
    } else {
      Arrays.sort(events, Comparator.comparingInt(e -> e[0]));
      int length = events.length;
      int[][] dp = new int[length + 1][k + 1];
      for (int i = length - 1; i >= 0; i--) {
        int next = this.binarySearch(events, events[i][1], i + 1, length);
        for (int j = 1; j <= k; j++) {
          dp[i][j] = Math.max(dp[i + 1][j], dp[next][j - 1] + events[i][2]);
        }
      }
      return dp[0][k];
    }
  }

  private int binarySearch(int[][] events, int target, int start, int end) {
    while (start < end) {
      int mid = ((end - start) / 2) + start;
      if (target >= events[mid][0]) {
        start = mid + 1;
      } else {
        end = mid;
      }
    }
    return start;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-number-of-events-that-can-be-attended-ii/submissions/1690571829/){:target="_blank"}

# 설명
1. 아래 구성으로 된 events를 이용하여 겹치지 않은 이벤트에 참석하여 얻을 수 있는 최대 값을 반환하는 문제이다.
- events[i] = [startDay<sub>i</sub>, endDay<sub>i</sub>, value<sub>i</sub>]로 구성되어 있으며, 각 값은 아래의 의미를 가진다.
  - startDay<sub>i</sub>는 i번째 이벤트 시작 날자를 의미한다.
  - endDay<sub>i</sub>는 i번째 이벤트 종료 날자를 의미한다.
  - value<sub>i</sub>는 i번째 이벤트 참석을 통해 얻을 수 있는 값을 의미한다.

2. k가 1인 하나의 이벤트만 참석하는 경우, 모든 이벤트 중 가장 큰 value 값을 주어진 문제의 결과로 반환한다.

3. events를 시작 날자인 첫 값 기준으로 오름차순 정렬한다.

4. 문제 풀이에 필요한 변수를 정의한다.
- length는 events의 길이를 저장한 변수이다.
- dp는 최대 값을 구하기 위한 배열로, $(length + 1) \times (k + 1)$ 크기의 2차원 배열로 초기화한다.

5. $length - 1$부터 0 이상까지 i를 감소시키며 아래를 반복한다.
- next에 $i + 1$번째 이벤트에서 마지막 이벤트까지 i번째 events의 종료 날자 이후에 시작하는 이벤트의 위치를 찾아 넣어준다.
- 1부터 k이하까지 j를 증가시키며 dp[i][j]의 위치에 dp[$i + 1$][k] 값인 다음 이벤트까지의 값과 $dp[next][j - 1] + events[i][2]$의 값인 해당 이벤트를 포함한 값의 합 중 큰 값을 넣어준다.

6. 반복이 완료되면 조건을 만족하는 최대 값이 저장된 dp[0][k]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumNumberOfEventsThatCanBeAttendedII.java){:target="_blank"}에서 확인 가능합니다.