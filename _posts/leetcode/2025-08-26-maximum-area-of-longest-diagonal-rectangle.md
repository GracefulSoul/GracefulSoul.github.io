---
title: "Leetcode Java Maximum Area of Longest Diagonal Rectangle"
excerpt: "Leetcode - 'Maximum Area of Longest Diagonal Rectangle' 문제 Java 풀이"
last_modified_at: 2025-08-26T18:50:00
header:
  image: /assets/images/leetcode/maximum-area-of-longest-diagonal-rectangle.png
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
[Link](https://leetcode.com/problems/maximum-area-of-longest-diagonal-rectangle/){:target="_blank"}

# 코드
```java
class Solution {

  public int areaOfMaxDiagonal(int[][] dimensions) {
    int result = 0;
    int max = 0;
    for (int[] dimension : dimensions) {
      int diagonal = (dimension[0] * dimension[0]) + (dimension[1] * dimension[1]);
      int area = dimension[0] * dimension[1];
      if (max < diagonal || (diagonal == max && result < area)) {
        max = diagonal;
        result = area;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-area-of-longest-diagonal-rectangle/submissions/1748833504/){:target="_blank"}

# 설명
1. dimensions는 사각형의 두 변의 값들로 저장된 2차원 배열로, 가장 긴 길이의 대각선 길이를 가진 사각형의 면적을 반환한다.
- 대각선의 길이가 동일한 경우, 가장 큰 면적을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과로 반환할 가장 큰 너비를 저장할 변수로, 0으로 초기화한다.
- max는 제곱근을 수행하지 않은 가장 큰 대각선의 길이를 저장할 변수로, 0으로 초기화한다.
  - 제곱근을 수행하지 않은 값이 더 큰 경우, 대각선의 길이도 더 길어 제곱근을 수행하지 않은 값으로 비교한다.

3. dimensions의 각 값을 순차적으로 dimension에 넣어 아래를 수행한다.
- 검증에 필요한 두 변수를 정의한다.
  - diagonal은 dimension의 제곱근을 수행하지 않은 대각선의 길이를 저장한 변수로, $dimension[0]^2 + dimension[1]^2$의 값으로 초기화한다.
  - area는 dimension의 면적을 저장할 변수로, $dimension[0] \times dimension[1]$의 값으로 초기화한다.
- 아래의 두 경우 중 하나라도 만족하면 max에 diagonal의 값을 넣어주고, result에 area를 넣어준다.
  - 현재 대각선의 길이인 diagonal의 값이 기존 가장 긴 대각선의 길이인 max의 값보다 더 큰 경우.
  - 현재 대각선의 길이인 diagonal의 값과 기존 가장 긴 대각선의 길이인 max의 값이 동일하면서 area의 값이 result보다 더 큰 면적인 경우.

4. 반복이 완료되면 조건에 만족하는 면적이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumAreaOfLongestDiagonalRectangle.java){:target="_blank"}에서 확인 가능합니다.