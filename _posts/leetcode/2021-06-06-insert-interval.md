---
title: "Leetcode Java Insert Interval"
excerpt: "Leetcode Insert Interval Java 풀이"
last_modified_at: 2021-06-06T16:00:00
header:
  image: /assets/images/leetcode/insert-interval.png
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
[Link](https://leetcode.com/problems/insert-interval/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] insert(int[][] intervals, int[] newInterval) {
    List<int[]> result = new ArrayList<>();
    for (int i = 0; i < intervals.length; i++) {
      if (intervals[i][0] > newInterval[1]) {
        result.add(newInterval);
        newInterval = intervals[i];
      } else if (intervals[i][1] >= newInterval[0]) {
        newInterval = new int[] { Math.min(intervals[i][0], newInterval[0]), Math.max(intervals[i][1], newInterval[1]) };
      } else {
        result.add(intervals[i]);
      }
    }
    result.add(newInterval);
    return result.toArray(new int[result.size()][]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/503746870/){:target="_blank"}

# 설명
1. 주어진 2차원 배열 intervals은 구간을 저장한 배열로, 주어진 newInterval 배열을 intervals에 포함시키는 문제이다.

2. 결과를 제출할 result 변수를 정의한다.
- 주어진 배열 newInterval이 intervals의 구간에 포함될지, 추가될지 몰라 정확한 배열의 크기를 초기에 확인하기 어려우므로 컬렉션으로 저장한다.

3. 주어진 배열 intervals를 반복하여 newInterval을 적용한다.
- intervals[i][0]이 newInterval[1]보다 큰 경우, 해당 구간보다 작은 구간이므로 result에 newInterval을 추가하고 newInterval에 intervals[i]값을 넣는다.
- intervals[i][1]이 newInterval[0]보다 크거나 같은 경우, 해당 구간에 포함되는 경우이므로, 새로운 구간을 생성한다.
  - intervals의 시작 값과 newInterval의 시작 값 중 작은 값을 새로운 구간의 시작 값으로 설정한다.
  - intervals의 종료 값과 newInterval의 종료 값 중 큰 값을 새로운 구간의 종료 값으로 설정한다.
- 그 외의 경우는 result에 intervals[i]를 추가한다.

4. 반복이 종료되면, 마지막으로 newInterval을 result에 추가해준다.
- 구간의 적용을 위해 임시 저장된 구간이므로, 반드시 포함시켜야 한다.

5. 새로운 구간들을 저장한 컬렉션인 result를 배열로 변경하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/InsertInterval.java){:target="_blank"}에서 확인 가능합니다.