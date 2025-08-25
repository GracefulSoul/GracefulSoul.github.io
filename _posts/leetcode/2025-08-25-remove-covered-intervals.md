---
title: "Leetcode Java Remove Covered Intervals"
excerpt: "Leetcode - 'Remove Covered Intervals' 문제 Java 풀이"
last_modified_at: 2025-08-25T18:20:00
header:
  image: /assets/images/leetcode/remove-covered-intervals.png
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
[Link](https://leetcode.com/problems/remove-covered-intervals/){:target="_blank"}

# 코드
```java
class Solution {

  public int removeCoveredIntervals(int[][] intervals) {
    Arrays.sort(intervals, (i, j) -> (i[0] == j[0] ? j[1] - i[1] : i[0] - j[0]));
    int result = 0;
    int curr = 0;
    for (int[] interval : intervals) {
      if (curr < interval[1]) {
        curr = interval[1];
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/remove-covered-intervals/submissions/1747538512/){:target="_blank"}

# 설명
1. 아래의 값이 저장된 intervals를 이용하여 다른 값에 포함된 범위 값들을 제거하고 남은 값의 갯수를 계산하는 문제이다.
- intervals[i] = [l<sub>i</sub>, r<sub>i</sub>] 로, l<sub>i</sub> 부터 r<sub>i</sub> 까지 범위를 나타낸다.

2. intervals의 값을 시작 값이 동일하면 종료 값이 큰 순서로, 아니면 시작 값이 작은 순서로 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- result는 남은 범위 값을 저장할 변수로, 0으로 초기화한다.
- curr은 종료 값을 저장할 변수로, 0으로 초기화한다.

4. intervals의 각 값을 순차적으로 interval에 넣어 아래를 수행한다.
- 현재 우측 범위가 저장된 curr의 값보다 interval[1]의 값이 큰 미포함 범위 값인 경우, curr에 interval[1]의 값을 넣고 result를 증가시켜준다.

5. 반복이 완료되면 남은 값의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveCoveredIntervals.java){:target="_blank"}에서 확인 가능합니다.