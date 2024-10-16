---
title: "Leetcode Java Divide Intervals Into Minimum Number of Groups"
excerpt: "Leetcode Divide Intervals Into Minimum Number of Groups Java"
last_modified_at: 2024-10-12T09:10:00
header:
  image: /assets/images/leetcode/divide-intervals-into-minimum-number-of-groups.png
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
[Link](https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups/){:target="_blank"}

# 코드
```java
class Solution {

  public int minGroups(int[][] intervals) {
    int length = intervals.length;
    int[] left = new int[length];
    int[] right = new int[length];
    for (int i = 0; i < length; i++) {
      left[i] = intervals[i][0];
      right[i] = intervals[i][1];
    }
    Arrays.sort(left);
    Arrays.sort(right);
    int result = 0;
    for (int i = 0, j = 0; i < length; i++) {
      if (left[i] <= right[j]) {
        result++;
      } else {
        j++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups/submissions/1419482524/){:target="_blank"}

# 설명
1. intervals를 이용하여 각 구간이 겹치지 않도록 나눌 수 있는 최소 그룹의 수를 구하는 문제이다.
- intervals[i] = [left<sub>i</sub>, right<sub>i</sub>]로, [left, right] 구간을 의미한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 intervals의 길이를 저장한 변수이다.
- left와 right는 각 intervals의 left, right 값을 저장할 변수로, length 크기의 정수 배열로 초기화하고 intervals를 이용하여 순차적으로 값을 넣어준 후 오름차순 정렬을 수행한다.
- result는 나눌 수 있는 최소 그룹의 수 저장할 변수로, 0으로 초기화한다.

3. i는 0부터 length 미만까지, j는 0으로 초기화하여 아래를 반복한다.
- left[i]의 값이 right[j]의 값보다 작은 경우, 그룹을 나눌 수 있으므로 result를 증가시킨다.
- 위의 경우가 아니라면 기존 그룹에 넣을 수 있으므로, j를 증가시켜준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DivideIntervalsIntoMinimumNumberOfGroups.java){:target="_blank"}에서 확인 가능합니다.