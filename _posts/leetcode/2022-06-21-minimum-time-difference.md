---
title: "Leetcode Java Minimum Time Difference"
excerpt: "Leetcode Minimum Time Difference Java"
last_modified_at: 2022-06-21T19:40:00
header:
  image: /assets/images/leetcode/minimum-time-difference.png
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
[Link](https://leetcode.com/problems/minimum-time-difference/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMinDifference(List<String> timePoints) {
    boolean[] visited = new boolean[1440];
    int start = Integer.MAX_VALUE;
    for (String timePoint : timePoints) {
      String[] time = timePoint.split(":");
      int minutes = Integer.parseInt(time[0]) * 60 + Integer.parseInt(time[1]);
      if (visited[minutes]) {
        return 0;
      } else {
        start = Math.min(start, minutes);
        visited[minutes] = true;
      }
    }
    int prev = start;
    int result = Integer.MAX_VALUE;
    for (int idx = start + 1; idx < 1440; idx++) {
      if (visited[idx]) {
        result = Math.min(result, idx - prev);
        prev = idx;
      }
    }
    return Math.min(result, Math.abs(prev - start - 1440));
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/727510114/){:target="_blank"}

# 설명
1. 시간을 저장한 timePoints 내 가장 작게 차이나는 두 시간의 차이를 분 단위로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- visited는 timePoints의 모든 값의 방문 여부를 저장하기 위한 배열로, 하루의 총 시간인 $24 \times 60 = 1440$ 크기로 정의한다.
- start는 가장 작은 시간의 위치를 분 단위로 저장하기 위한 변수로, Integer의 가장 큰 숫자로 정의한다.

3. timePoints의 모든 값을 반복하여 아래를 수행한다.
- timePoint의 시간과 분의 구분 값인 콜론(":")을 기준으로 문자열을 분리한다.
- 시간을 분으로 변환한 값을 넣을 minutes에 time을 이용하여 시간의 위치인 time[0]을 숫자로 변환하여 60을 곱하고, 분의 위치인 time[1]을 숫자로 변환하여 더한 값을 넣어준다.
- visited의 minutes번째 값이 true인 경우 같은 시간이 존재하므로, 두 시간의 차이인 0을 주어진 문제의 결과로 반환한다.
- visited의 minutes번째 값이 false인 경우 같은 값이 없으므로, start에 start와 minutes 중 작은 값을 넣고 visited의 minutes번째 값을 true로 바꾸어준다.

4. 이전 값을 저장할 prev에 start를 넣어주고, result를 Integer의 가장 큰 숫자로 넣어 초기화한다.

5. $start + 1$부터 1440 미만까지 idx를 증가시키며 아래를 수행한다.
- visited의 idx번째 값이 true인 경우, result에 시간의 차이가 작은 값을 넣기 위해 result와 $idx - prev$ 값 중 작은 값을 넣어주고 prev에 idx를 넣어준다.

6. 반복이 완료되면 연속된 시간 중 가장 작은 result와 처음과 마지막 시간의 차이인 $prev - start - 1440$ 중 작은 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumTimeDifference.java){:target="_blank"}에서 확인 가능합니다.