---
title: "Leetcode Java Rectangle Overlap"
excerpt: "Leetcode - 'Rectangle Overlap' 문제 Java 풀이"
last_modified_at: 2023-02-11T12:30:00
header:
  image: /assets/images/leetcode/rectangle-overlap.png
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
[Link](https://leetcode.com/problems/rectangle-overlap){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isRectangleOverlap(int[] rec1, int[] rec2) {
    return rec1[0] < rec2[2] && rec2[0] < rec1[2] && rec1[1] < rec2[3] && rec2[1] < rec1[3];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/image-overlap/submissions/895688314/){:target="_blank"}

# 설명
1. 두 사각형 좌표를 이용하여 겹치는 구간이 있는지 검증하는 문제이다.
- rec는 [x1, y1, x2, y2]이며, 좌측 하단 모서리 좌표인 (x1, y1)과 우측 상단 모서리 좌표인 (x2, y2)로 구성되어 있다.

2. 아래의 각 모서리 좌표를 이용하여 모두 만족하여 겹치는 구간이 존재하는지를 검증한 결과를 반환한다.
- rec1의 첫 번째 값인 좌측 하단 모서리 x축 좌표보다 rec2의 세 번째 값인 우측 상단의 모서리 x축 좌표가 더 큰 경우.
- rec2의 첫 번째 값인 좌측 하단 모서리 x축 좌표보다 rec1의 세 번째 값인 우측 상단의 모서리 x축 좌표가 더 큰 경우.
- rec1의 두 번째 값인 좌측 하단 모서리 y축 좌표보다 rec2의 네 번째 값인 우측 상단의 모서리 y축 좌표가 더 큰 경우.
- rec2의 두 번째 값인 좌측 하단 모서리 y축 좌표보다 rec1의 네 번째 값인 우측 상단의 모서리 y축 좌표가 더 큰 경우.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RectangleOverlap.java){:target="_blank"}에서 확인 가능합니다.