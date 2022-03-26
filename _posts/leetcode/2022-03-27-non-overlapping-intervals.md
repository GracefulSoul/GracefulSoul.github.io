---
title: "Leetcode Java Non-overlapping Intervals"
excerpt: "Leetcode Non-overlapping Intervals Java 풀이"
last_modified_at: 2022-03-27T08:00:00
header:
  image: /assets/images/leetcode/non-overlapping-intervals.png
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
[Link](https://leetcode.com/problems/non-overlapping-intervals/){:target="_blank"}

# 코드
```java
class Solution {

  public int eraseOverlapIntervals(int[][] intervals) {
    Arrays.sort(intervals, (interval1, interval2) -> {
      return interval1[1] - interval2[1];
    });
    int end = intervals[0][1];
    int count = 1;
    for (int[] interval : intervals) {
      if (interval[0] >= end) {
        end = interval[1];
        count++;
      }
    }
    return intervals.length - count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/667891646/){:target="_blank"}

# 설명
1. 배열 intervals가 주어지면 겹치지 않은 구간을 만들기 위해 제거해야 하는 값들의 갯수를 구하는 문제이다.
- intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]

2. intervals를 end 값 기준으로 오름차순 정렬을 수행한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- end는 중복되지 않은 구간을 구하기 위한 값을 임시 저장할 변수로, intervals의 첫 값의 두 번째 값인 end 값으로 초기화한다.
- count는 중복되지 않은 구간을 세기 위한 변수로, 1로 초기화한다.

4. intervals를 반복하여 count를 계산한다.
- interval의 첫 값이 end보다 크거나 같은 경우, end에 interval의 두 번째 값을 넣어주고 count를 증가시킨다.

5. intervals의 크기에 중복되지 않은 구간의 갯수인 count를 빼서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NonOverlappingIntervals.java){:target="_blank"}에서 확인 가능합니다.