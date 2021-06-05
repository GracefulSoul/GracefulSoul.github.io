---
title: "Leetcode Java Merge Intervals"
excerpt: "Leetcode Merge Intervals Java 풀이"
last_modified_at: 2021-06-05T19:30:00
header:
  image: /assets/images/leetcode/jump-game.png
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
[Link](https://leetcode.com/problems/jump-game/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] merge(int[][] intervals) {
    if (intervals.length == 1) {
      return intervals;
    }
    Arrays.sort(intervals, (i1, i2) -> i1[0] - i2[0]);
    List<int[]> result = new ArrayList<>();
    result.add(intervals[0]);
    for (int[] interval : intervals) {
      int[] temp = result.get(result.size() - 1);
      if (temp[1] >= interval[0]) {
        temp[1] = Math.max(temp[1], interval[1]);
      } else {
        result.add(interval);
      }
    }
    return result.toArray(new int[result.size()][]);
  }
}
```

# 결과
[Link](https://leetcode.com/submissions/detail/503310440/){:target="_blank"}

# 설명
1. 주어진 2차원 배열 intervals을 이용하여 각 구간이 중첩되지 않은 구간들로 변경하는 문제이다.

2. 만일 intervals의 크기가 1이라면, 구간이 중첩되지 않으므로 intervals를 주어진 문제의 결과로 반환한다.

3. 주어진 배열 intervals의 첫 값을 기준으로 정렬을 수행한다.
- 주어진 배열 intervals의 내부 배열의 값은 시작 값, 종료 값으로 2개의 숫자로 구성되어 있으므로, 구간의 중첩을 명확하게 구분하기 위해서는 시작 값을 기준으로 정렬을 수행한다.

4. 중첩되지 않은 구간들을 저장할 컬렉션 result를 정의한다.
- 중첩되지 않은 구간들을 구할 때, 정확한 배열의 크기를 초기에 확인하기 어려우므로 컬렉션으로 저장한다.

5. 주어진 배열 intervals의 첫 값을 result에 저장하고, intervals를 반복하여 중첩되지 않은 구간들을 탐색한다.
- 임시 변수로 사용할 배열 temp에 변수 result에 마지막 값을 가져와서 임시 저장한다.
- 배열 temp의 종료 값과 주어진 배열 intervals의 배열 내 값인 interval의 시작 값을 비교하여 temp의 종료 값이 크거나 같은 경우 구간이 중첩되므로, temp[1]에 temp[1]과 interval[1] 중 큰 값을 저장한다.
- 위의 경우가 아닌 경우 구간이 중첩되지 않으므로, result에 interval 값을 저장한다.

6. 반복이 종료되면 중첩되지 않은 구간들을 저장한 컬렉션인 result를 배열로 변경하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MergeIntervals.java){:target="_blank"}에서 확인 가능합니다.