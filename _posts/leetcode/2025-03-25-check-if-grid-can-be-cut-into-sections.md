---
title: "Leetcode Java Check if Grid can be Cut into Sections"
excerpt: "Leetcode - 'Check if Grid can be Cut into Sections' 문제 Java 풀이"
last_modified_at: 2025-03-25T20:30:00
header:
  image: /assets/images/leetcode/check-if-grid-can-be-cut-into-sections.png
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
[Link](https://leetcode.com/problems/check-if-grid-can-be-cut-into-sections/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkValidCuts(int n, int[][] rectangles) {
    return this.checkValidCuts(rectangles, 0) || this.checkValidCuts(rectangles, 1);
  }

  private boolean checkValidCuts(int[][] rectangles, int i) {
    int result = 0;
    Arrays.sort(rectangles, (a, b) -> Integer.compare(a[i], b[i]));
    int prev = rectangles[0][i + 2];
    for (int[] rectangle : rectangles) {
      if (prev <= rectangle[i]) {
        result++;
      }
      prev = Math.max(prev, rectangle[i + 2]);
    }
    return result > 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-grid-can-be-cut-into-sections/submissions/1585531018/){:target="_blank"}

# 설명
1. $n \times n$ 크기의 정사각형 내 아래의 조건을 만족하는 직사각형 위치가 저장된 rectangles를 이용하여 가로 혹은 세로로 두 번 절단 가능한지 검증하는 문제이다.
- rectangles[i] = [start<sub>x</sub>, start<sub>y</sub>, end<sub>x</sub>, end<sub>y</sub>]로 직사각형의 x축은 start<sub>x</sub>부터 시작하여 end<sub>x</sub>까지, y축은 start<sub>y</sub>부터 end<sub>y</sub>까지로 의미한다.

2. rectangles의 가로와 세로 기준으로 정렬하여 두 번 절단 가능한지 검증하기 위한 checkValidCuts(int[][] rectangles, int i) 메서드를 정의한다.
- result는 절단 갯수를 저장하기 위한 변수로, 0으로 초기화한다.
- rectangles를 i 기준의 위치 값 기준으로 오름차순 정렬해준다.
- prev는 이전 직사각형의 종료 위치를 저장할 변수로, rectangles[0][$i + 2$]인 첫 직사각형의 종료 위치를 저장한다.
- rectangles 정렬된 순서대로 rectangle에 넣어 아래를 수행한다.
  - prev의 값이 rectangle[i] 값인 시작 위치보다 작거나 같은 절단 가능한 경우, result를 증가시켜준다.
  - prev에 prev와 rectangle[i + 2] 값인 종료 위치 중 큰 값을 넣어준다.
- result가 1 초과인 두 번 절단 가능한 위치가 존재하는지 여부를 반환한다.

3. 2번에서 정의한 checkValidCuts(int[][] rectangles, int i) 메서드를 0과 1인 x의 시작 위치와 y의 시작 위치를 이용하여 수행한 결과 중 하나라도 참인지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfGridCanBeCutIntoSections.java){:target="_blank"}에서 확인 가능합니다.