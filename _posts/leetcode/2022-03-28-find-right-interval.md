---
title: "Leetcode Java Find Right Interval"
excerpt: "Leetcode Find Right Interval Java 풀이"
last_modified_at: 2022-03-28T17:00:00
header:
  image: /assets/images/leetcode/find-right-interval.png
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
[Link](https://leetcode.com/problems/find-right-interval/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findRightInterval(int[][] intervals) {
    int min = Integer.MAX_VALUE;
    int max = Integer.MIN_VALUE;
    for (int[] interval : intervals) {
      min = Math.min(min, interval[0]);
      max = Math.max(max, interval[1]);
    }
    int[] map = new int[max - min + 1];
    for (int idx = 0; idx < map.length; idx++) {
      map[idx] = Integer.MIN_VALUE;
    }
    for (int idx = 0; idx < intervals.length; idx++) {
      map[intervals[idx][0] - min] = idx;
    }
    for (int idx = map.length - 2; idx >= 0; idx--) {
      if (map[idx] == Integer.MIN_VALUE) {
        map[idx] = map[idx + 1];
      }
    }
    int[] result = new int[intervals.length];
    for (int idx = 0; idx < intervals.length; idx++) {
      int val = map[intervals[idx][1] - min];
      if (val == Integer.MIN_VALUE) {
        result[idx] = -1;        
      } else {
        result[idx] = val;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/667891646/){:target="_blank"}

# 설명
1. 배열 intervals가 주어지면 각각 우측에 위치하는 interval을 찾아 위치를 넣어 반환하는 문제이다.
- intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]
- 단, start<sub>i</sub>는 배열 내 고유한 값이다.
- intervals[i]에 대한 오측에 위치하는 interval은 start<sub>j</sub> >= end<sub>i</sub>이고 start<sub>j</sub>가 최소화되는 intervals[j]이며, i와 j가 같을 수 있다.
- intervals[i]에 대한 우측에 위치하는 interval이 없을 경우, -1을 해당 자리에 넣는다.

2. 문제 풀이에 필요한 변수를 정의한다.
- min은 시작 값이 가장 작은 값을 저장하기 위한 변수로, interval의 첫 번째 값들 중 가장 작은 값을 찾아 넣어준다.
- max는 끝 값이 가장 큰 값을 저장하기 위한 변수로, interval의 두 번째 값들 중 가장 큰 값을 찾아 넣어준다.
- map은 해당 구간내 위치를 지정하기 위한 배열로, 최소 크기가 되는 $max - min + 1$ 크기로 정의하고 모든 위치에 정수의 가장 작은 값을 넣어준다.

3. 0부터 intervals 길이 미만까지 반복하여 아래를 수행한다.
- map의 $intervals[idx][0] - min$ 위치에 순서인 idx를 넣어준다.

4. map을 뒤에서부터 idx를 감소시키며 아래를 수행한다.
- map의 idx번째 값이 정수의 가장 작은 값인 경우, $idx + 1$번째에 있는 값을 넣어준다.

5. 결과를 넣어줄 result 배열을 intervals의 크기로 정의하고, 0부터 해당 크기 미만까지 idx를 증가시키며 반복하여 아래를 수행한다.
- map의 $intervals[idx][1] - min$번째 값을 val에 넣어준다.
- val이 정수의 가장 작은 값인 경우 우측에 존재하는 값이 없으므로, result의 idx번째 위치에 -1을 넣어준다.
- 위의 경우가 아니면, result의 idx번째 위치에 val을 넣어준다.

6. 반복이 완료되면 각각 우측에 위치하는 interval의 위치 값을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NonOverlappingIntervals.java){:target="_blank"}에서 확인 가능합니다.