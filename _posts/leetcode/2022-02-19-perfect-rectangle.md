---
title: "Leetcode Java Perfect Rectangle"
excerpt: "Leetcode Perfect Rectangle Java 풀이"
last_modified_at: 2022-02-19T18:00:00
header:
  image: /assets/images/leetcode/perfect-rectangle.png
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
[Link](https://leetcode.com/problems/perfect-rectangle/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isRectangleCover(int[][] rectangles) {
    Set<int[]> rectangleSet = new TreeSet<>((r1, r2) -> {
      if (r1[1] >= r2[3] || r1[0] >= r2[2]) {
        return 1;
      } else if (r1[3] <= r2[1] || r1[2] <= r2[0]) {
        return -1;
      } else {
        return 0;
      }
    });
    int top = Integer.MIN_VALUE;
    int bottom = Integer.MAX_VALUE;
    int left = Integer.MAX_VALUE;
    int right = Integer.MIN_VALUE;
    int area = 0;
    for (int[] rectangle : rectangles) {
      if (!rectangleSet.add(rectangle)) {
        return false;
      }
      area += (rectangle[2] - rectangle[0]) * (rectangle[3] - rectangle[1]);
      top = Math.max(top, rectangle[3]);
      bottom = Math.min(bottom, rectangle[1]);
      left = Math.min(left, rectangle[0]);
      right = Math.max(right, rectangle[2]);
    }
    return (right - left) * (top - bottom) == area;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/644396729/){:target="_blank"}

# 설명
1. 주어진 2차원 정수 배열 rectangles는 직사각형들의 좌표 값으로, 해당 직사각형들을 이용하여 겹치지 않은 정사각형을 만들 수 있는지를 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- rectangleSet은 중복을 배제하고 정렬된 이진 탐색 트리 형태로 저장하기 위해 [TreeSet](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html){:target="_blank"}으로 정의한다.
- top과 right는 가장 작은 값을 넣기 위해 정수의 최솟값으로 넣어 정의한다.
- bottom과 left는 가장 큰 값을 넣기 위해 정수의 최댓값으로 넣어 정의한다.
- area는 각 사각형의 부피를 넣기 위한 변수로, 0으로 정의한다.

3. 주어진 rectangles를 반복하여 부피와 좌표를 정의한다.
- rectangleSet에 rectangle이 겹치는 경우, false를 반환한다.
- area에 x축의 차이와 y축의 차이를 곱한 rectangle의 부피를 더해준다.
- top과 right에 자신의 값과 각 좌표의 크기 중 큰 값을 넣어준다.
- bottom과 left에 자신의 값과 각 좌표의 큰기 중 작은 값을 넣어준다.

4. 각 좌표값을 이용한 부피의 크기와 area의 크기가 동일한지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PerfectRectangle.java){:target="_blank"}에서 확인 가능합니다.