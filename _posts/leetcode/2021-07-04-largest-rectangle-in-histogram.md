---
title: "Leetcode Java Largest Rectangle in Histogram"
excerpt: "Leetcode Largest Rectangle in Histogram Java 풀이"
last_modified_at: 2021-07-04T16:30:00
header:
  image: /assets/images/leetcode/largest-rectangle-in-histogram.png
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
[Link](https://leetcode.com/problems/largest-rectangle-in-histogram/){:target="_blank"}

# 코드
```java
class Solution {

  public int largestRectangleArea(int[] heights) {
    int maxArea = 0;
    Stack<Integer> stack = new Stack<>();
    for (int idx = 0; idx < heights.length; idx++) {
      maxArea = this.getMaxArea(heights, stack, maxArea, idx);
      stack.push(idx);
    }
    return this.getMaxArea(heights, stack, maxArea, heights.length);
  }
  
  private int getMaxArea(int[] heights, Stack<Integer> stack, int maxArea, int idx) {
    int _maxArea = maxArea;
    while (!stack.isEmpty() && (idx == heights.length || heights[idx] < heights[stack.peek()])) {
      int height = heights[stack.pop()];
      int start = stack.isEmpty() ? -1 : stack.peek();
      _maxArea = Math.max(_maxArea, height * (idx - start - 1));
    }
    return _maxArea;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/517137461/){:target="_blank"}

# 설명
1. 주어진 배열 heights는 히스토그램의 바의 높이이며, x축과 y축의 곱의 영역이 가장 큰 영역의 크기를 구하는 문제이다.

2. 주어진 문제를 풀기 위한 두 변수를 정의한다.
- 최대 영역의 크기를 저장하는 maxArea를 정의한다.
- 최대 영역을 구하기 위한 시작 index를 FIFO로 저장할 Stack인 stack을 정의한다.

3. 주어진 heights의 값들을 모두 반복하여 최대 길이를 저장한다.
- 아래의 경우에 해당하지 않을 경우, stack의 내부 값을 활용하여 최대 길이를 구한다.
  - stack이 비어있지 않을 경우, 최대 영역을 구하기 위한 index가 저장되었을 경우이다.
  - idx와 heights의 길이가 동일하거나 heights[idx]의 값이 heights[stack.peek()]의 값보다 작을 경우, 길이가 작아지는 구간이므로 이전의 값을 이용하여 최대 길이를 확인한다.
- 변수 maxArea와 저장된 공통 높이인 heights[stack.pop()]에 $idx - start - 1$의 값을 곱해준다.
  - start는 stack이 비어있을 경우 height의 높이가 처음 index부터 시작되므로, -1을 사용한다.
  - 위의 경우가 아닌 경우 height의 높이가 시작되는 index가 존재하는 경우이므로, stack.pop()을 통해 stack에 저장된 이전 구간의 값을 가져온다.
- stack에 해당 위치인 idx를 넣어준다.

4. 반복이 완료되면, 3번을 다시 반복하여 stack에 저장된 값을 활용해서 최대 길이를 다시 확인하고 해당 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestRectangleInHistogram.java){:target="_blank"}에서 확인 가능합니다.