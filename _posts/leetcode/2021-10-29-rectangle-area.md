---
title: "Leetcode Java Rectangle Area"
excerpt: "Leetcode - 'Rectangle Area' 문제 Java 풀이"
last_modified_at: 2021-10-29T12:00:00
header:
  image: /assets/images/leetcode/rectangle-area.png
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
[Link](https://leetcode.com/problems/rectangle-area/){:target="_blank"}

# 코드
```java
class Solution {

  public int computeArea(int ax1, int ay1, int ax2, int ay2, int bx1, int by1, int bx2, int by2) {
int left = Math.max(ax1, bx1);
    int x = Math.min(ax2, bx2) - Math.max(ax1, bx1);
    int y = Math.min(ay2, by2) - Math.max(ay1, by1);
    if (x > 0 && y > 0) {
      return ((ax2 - ax1) * (ay2 - ay1)) + ((bx2 - bx1) * (by2 - by1)) - (x * y);
    } else {
      return ((ax2 - ax1) * (ay2 - ay1)) + ((bx2 - bx1) * (by2 - by1));
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/578779691/){:target="_blank"}

# 설명
1. 주어진 좌표 정보들을 이용하여 a와 b 두 사각형으로 만들어진 2차원 공간의 부피를 구하는 문제이다.

2. 문제를 풀기위한 변수를 정의한다.
- x는 ax와 bx의 각 위치를 이용하여 겹쳐진 공간의 x축 길이를 넣어준다.
- y는 ay와 by의 각 위치를 이용하여 겹쳐진 공간의 y축 길이를 넣어준다.

3. x와 y의 길이에 따라 주어진 문제의 결과를 반환한다.
- x와 y의 길이가 0보다 클 경우, 사각형 a와 b의 겹쳐진 공간이 존재하므로 사각형 a와 b의 부피의 합에 겹쳐진 공간의 부피인 $x \times y$의 값을 빼서 주어진 문제의 결과로 반환한다.
- x 혹은 y의 길이가 0보다 작을 경우, 사각형 a와 b의 겹쳐진 공간이 존재하지 않으므로, a와 b의 부피의 합을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RectangleArea.java){:target="_blank"}에서 확인 가능합니다.