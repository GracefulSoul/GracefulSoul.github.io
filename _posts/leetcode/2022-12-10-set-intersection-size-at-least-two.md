---
title: "Leetcode Java Set Intersection Size At Least Two"
excerpt: "Leetcode - 'Set Intersection Size At Least Two' 문제 Java 풀이"
last_modified_at: 2022-12-10T15:20:00
header:
  image: /assets/images/leetcode/set-intersection-size-at-least-two.png
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
[Link](https://leetcode.com/problems/set-intersection-size-at-least-two){:target="_blank"}

# 코드
```java
class Solution {

  public int intersectionSizeTwo(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[1] != b[1] ? a[1] - b[1] : b[0] - a[0]);
    int start = intervals[0][1] - 1;
    int end = intervals[0][1];
    int size = 2;
    for (int idx = 1; idx < intervals.length; idx++) {
      if (intervals[idx][0] > start && intervals[idx][0] <= end) {
        start = end;
        end = intervals[idx][1];
        size++;
      } else if (intervals[idx][0] > end) {
        start = intervals[idx][1] - 1;
        end = intervals[idx][1];
        size += 2;
      }
    }
    return size;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/set-intersection-size-at-least-two/submissions/857436052/){:target="_blank"}

# 설명
1. 정수 구간을 저장한 intervals의 각 구간 별 최소 두 개의 정수를 가지는 가장 작은 집합의 크기를 구하는 문제이다.
- intervals[i] = [start<sub>i</sub>, end<sub>i</sub>] 이며, 정수의 시작과 끝의 구간을 나타낸다.

2. intervals를 아래의 조건으로 정렬한다.
- 구간의 종료 위치가 동일하지 않은 경우, 종료 위치가 빠른 순서로 정렬한다.
- 구간의 종료 위치가 동일한 경우, 시작 위치가 늦은 순서로 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- start는 이전 시작 위치를 저장할 변수로, intervals의 첫 구간의 시작 위치로 초기화한다.
- end는 이전 종료 위치를 저장할 변수로, intervals의 첫 구간의 종료 위치로 초기화한다.
- size는 가장 작은 집합의 크기를 저장할 변수로, 앞의 두 값이 포함되었으므로 2로 초기화한다.

4. 첫 값은 변수 초기화에 사용하였으므로, 1부터 intervals의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- intervals의 idx번째 구간의 시작 위치가 start 보다 크고, 종료 위치가 end보다 작거나 같으면 아래를 수행한다.
  - start에 end를 넣어 시작 위치를 변경한다.
  - end에 intervals의 idx번째 구간의 종료 위치를 넣어 종료 위치를 변경한다.
  - 하나의 겹치는 구간이 발생하므로, size는 1만 증가시킨다.
- 위의 경우가 아니면서 intervals의 idx번째 구간의 시작 위치가 end보다 크면 구간이 겹치지 않으므로 아래를 수행한다.
  - start에 intervals의 idx번째 구간의 종료 위치보다 1 작은 값을 넣어준다.
  - end에 intervals의 idx번째 구간의 종료 위치를 넣어준다.
  - 구간이 겹치는 구간이 없으므로, 이전 구간에 2개의 값을 추가하여 size를 2 증가시킨다.

5. 반복이 완료되면 조건을 충족하는 최소 집합의 크기인 size를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SetIntersectionSizeAtLeastTwo.java){:target="_blank"}에서 확인 가능합니다.