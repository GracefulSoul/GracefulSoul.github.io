---
title: "Leetcode Java Maximal Rectangle"
excerpt: "Leetcode Maximal Rectangle Java 풀이"
last_modified_at: 2021-07-05T18:00:00
header:
  image: /assets/images/leetcode/maximal-rectangle.png
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
[Link](https://leetcode.com/problems/maximal-rectangle/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximalRectangle(char[][] matrix) {
    if (matrix.length == 0) {
      return 0;
    }
    int maxArea = 0;
    int[] heights = new int[matrix[0].length];
    for (char[] row : matrix) {
      for (int idx = 0; idx < row.length; idx++) {
        if (row[idx] == '1') {
          heights[idx]++;
        } else {
          heights[idx] = 0;
        }
      }
      maxArea = Math.max(maxArea, this.getMaxArea(heights, new Stack<>()));
    }
    return maxArea;
  }

  public int getMaxArea(int[] heights, Stack<Integer> stack) {
    int maxArea = 0;
    for (int idx = 0; idx <= heights.length; idx++) {
      while (!stack.isEmpty() && (idx == heights.length || heights[idx] < heights[stack.peek()])) {
        int height = heights[stack.pop()];
        int start = stack.isEmpty() ? -1 : stack.peek();
        maxArea = Math.max(maxArea, height * (idx - start - 1));
      }
      stack.push(idx);
    }
    return maxArea;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/517550977/){:target="_blank"}

# 설명
1. 주어진 2차원 배열 matrix를 이용하여 사각형 모양이 되는 부분 영역의 합이 가장 큰 값을 구하는 문제이다.

2. 주어진 matrix의 길이가 0인 경우, 문제 풀이가 불가능하므로 0을 주어진 문제의 결과로 반환한다.

3. 주어진 문제 풀이를 위해서 변수를 정의한다.
- maxArea는 최대 영역의 크기를 저장하기 위해서 0으로 정의한다.
- heights는 해당 문제를 Histogram 형식으로 전환하여 구하기 위해서 matrix[0]의 길이만큼의 크기로 int 배열을 정의한다.

4. 주어진 matrix를 이용하여 Histogram 형식으로 구간 별 heights를 만들어 최대 영역을 구한다.
- 셀의 값이 1일 경우 최대 영역을 구하기 위해서 heights[idx]의 값을 증가시킨다.
- 셀의 값이 0일 경우 heights[idx]의 값을 0으로 설정하여 새로운 영역을 구할 수 있도록 한다.
- 부분 영역의 최대 값을 저장하는 maxArea와 heights를 이용하여 최대 영역을 구한 값의 합 중 큰 값을 maxArea에 저장한다.
  - 아래의 경우가 모두 해당하는 경우, heights와 stack을 활용하여 최대 길이를 구한다.
    - stack이 비어있지 않을 경우, 최대 영역을 구하기 위한 index가 저장되었을 경우이다.
    - idx와 heights의 길이가 동일하거나 heights[idx]의 값이 heights[stack.peek()]의 값보다 작을 경우, 길이가 작아지는 구간이다.
  - 변수 maxArea와 저장된 공통 높이인 heights[stack.pop()]에 $idx - start - 1$의 값을 곱해준다.
    - start는 stack이 비어있을 경우 height의 높이가 처음 index부터 시작되므로, -1을 사용한다.
    - 위의 경우가 아닌 경우 height의 높이가 시작되는 index가 존재하는 경우이므로, stack.pop()을 통해 stack에 저장된 이전 구간의 값을 가져온다.
- stack에 해당 위치인 idx를 넣어주고 반복을 계속 진행하여 최대 영역을 구한다.

5. 반복이 완료되면 사각형 모양의 부분 영역의 합이 가장 큰 값을 저장한 maxArea의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximalRectangle.java){:target="_blank"}에서 확인 가능합니다.