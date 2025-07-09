---
title: "Leetcode Java Reschedule Meetings for Maximum Free Time I"
excerpt: "Leetcode - 'Reschedule Meetings for Maximum Free Time I' 문제 Java 풀이"
last_modified_at: 2025-07-09T23:00:00
header:
  image: /assets/images/leetcode/reschedule-meetings-for-maximum-free-time-i.png
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
[Link](https://leetcode.com/problems/reschedule-meetings-for-maximum-free-time-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxFreeTime(int eventTime, int k, int[] startTime, int[] endTime) {
    int length = startTime.length;
    int[] gaps = new int[length + 1];
    gaps[0] = startTime[0];
    gaps[length] = eventTime - endTime[length - 1];
    for (int i = 1; i < length; i++) {
      gaps[i] = startTime[i] - endTime[i - 1];
    }
    int window = 0;
    for (int i = 0; i <= k; i++) {
      window += gaps[i];
    }
    int result = window;
    for (int i = k + 1; i <= length; i++) {
      window += gaps[i] - gaps[i - (k + 1)];
      result = Math.max(result, window);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reschedule-meetings-for-maximum-free-time-i/submissions/1692037570/){:target="_blank"}

# 설명
1. [0, eventTime] 범위 내 i개의 스케줄 시작과 종료 시간이 저장된 startTime과 endTime을 이용해서 최대 k개의 스케줄 조정을 통해 얻을 수 있는 최대 여유 시간을 구하는 문제이다.
- 최대 여유 시간은 스케줄 사이의 유휴 시간을 의미하며, 각각의 스케줄은 겹치지 않아야 한다.
- 각 스케줄은 eventTime 외 시간으로 변경할 수 없다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 스케줄 갯수인 startTime의 길이를 저장한 변수이다.
- gaps는 스케줄 사이의 여유 시간을 저장할 배열로, $length + 1$ 크기의 정수 배열로 초기화 후 아래를 통해 값을 넣어준다.
  - gaps[0]에 startTime[0]의 값을, gaps[length]에 $eventTime - endTime[length - 1]$ 값을 넣어준다.
  - 1부터 length 미만까지 i를 증가시키며, gaps[i]에 $startTime[i] - endTime[i - 1]$의 값인 스케줄의 차잇값을 넣어준다.
- window는 Sliding Window 방식으로 결과 값 탐색하기 위한 변수로, 0으로 초기화 후 0부터 k 이하까지 i를 증가시키며, window에 gaps[i] 값을 더해준다.
- result는 결과 값을 저장할 변수로, 위에서 초기화한 window 값을 넣어준다.

4. $k + 1$부터 length 이하까지 i를 증가시키며 아래를 반복한다.
- window에 아래 두 값의 차잇값을 더해준다.
  - gaps[i] 값인 i번째 위치 이전까지 여유 시간.
  - gaps[$i - (k + 1)$] 값인 window 값을 구성할 때 옮긴 스케줄 이전의 여유 시간.
- result에 해당 값과 window 중 큰 값인 가장 큰 여유 시간을 넣어준다.

5. 반복이 완료되어 저장된 가장 큰 여유 시간이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RescheduleMeetingsForMaximumFreeTimeI.java){:target="_blank"}에서 확인 가능합니다.